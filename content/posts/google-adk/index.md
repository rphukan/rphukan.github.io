---
title: 'Build a Git PR Review agent using Google Agent Development Kit'
date: 2026-04-01T16:58:51+05:30
tags: ['Agent Development Kit', 'ADK', 'PR Review Agent']
image: 'adk.png'
draft: false
---
## **Google ADK**
#### **What is Google ADK?**
ADK is open sourced framework for developing agents which works with all the ppopular LLM models. It is also available in multiple languages like python, java and go. Using ADK you can create a multi-agent architecture where the primary agent can delegate the tasks to more specialized agents. You can also create agent workflows with agents in a parallel, sequencial or loop workflow. These agents can also use equiped with tools both pre-build as well as custom tools and MCP. ADK support other popular frameworks like LangChain and protocols like A2A.
#### **Setup**
We will be using python as our language of choice. ADK need `Python 3.11+` . Check your python version, if not available download it from [here](https://www.python.org/downloads/)

For python setup, open a terminal and 

```shell
mkdir agent-workspace
cd agent-workspace
# create a workspace folder and cd into it

python --version
# or python3 --version, expected output python 3.11.x or higher

python -m venv .venv
# create a virtual environment to isolate your project dependencies from the system installation.

source .venv/bin/activate # on mac
# on windows use .venv\Scripts\Activate.ps1 , this would activate the virtual environment
# if your terminal prompt starts with (.venv) now, you know that the virtual environment is activated

pip install google-adk
# this would install the adk framework, the adk cli and the dependent packages

adk --version
# should show version number like 1.0.0 or higher
```

Next you need the API key for your agent to call the LLM. Here we are going to use Google's Gemini models.
The simplest way to access Gemini is via Google AI Studio. For that you 
+ Visit [Google AI Studio](https://aistudio.google.com/apikey)
+ Sign in with your Google account
+ Click Create API Key
+ Copy the API key (it looks like `AIzaSyB.....`) and keep it safe.We will need it in the next step.

This is the quickest way where you also get the free tier benefits and hence works best for learning. But if you are looking for production setup, you would be doing it using `Google Cloud Vertex AI`


#### **A Simple Example Agent**
Before jumping into our use case, lets try a simple example.

```shell
adk create sample_agent

# the above adk cli command should create the below files in the current directory
sample_agent/
 ├── agent.py      # Main agent code (you’ll edit this)
 ├── __init__.py   # Python package initialization
 └── .env          # Environment variables (you’ll edit this next)
```

The `agent.py` is where you define your agent. Always assign your main agent to a variable named `root_agent` as ADK command-line tools look for a Python variable named root_agent as the entry point to your agent system. This is a convention that allows ADK to discover and run your agent.

```python
from google.adk.agents.llm_agent import Agent

root_agent = Agent(
    model='gemini-2.5-flash',
    # Model(Required): The LLM, the reasoning engine
    name='math_tutor_agent',
    # Identity(Required): Identifier for the agent. In a multi agent systems agents refer each other using this
    description='Helps students learn algebra by guiding them through problem solving steps.',
    # Purpose(Optional): A summary of what this agent does. 
    # Used by other agents to determine if they should route a task to this agent
    instruction='You are a very patient mathematics tutor. Your job is to help students in solving their algebra problems.',
    # Behavior(Optional but critical): The goal of the agent and how it should act
)
```

The `__init__.py` is a the python package initialization file that imports your agent module. This is required for ADK to discover your agent
```python
from . import agent
```

The `.env` file is the python environment file to place your environment variables.  Paste the API key that you created during the setup step. ADK would automatically load the environment varaiblesfrom  this file.
```python
GOOGLE_GENAI_USE_VERTEXAI=0  #if you created the API key from Google AI Studio. 
#If you use Vertex AI, this should be set to 1 and also provide GOOGLE_CLOUD_LOCATION and GOOGLE_CLOUD_PROJECT
GOOGLE_API_KEY=AIz.... # paste your API key here
```

If all the above steps are done, now its time to bring the agent to life. To keep it simple, we will use the ADK web interface to run the agent for now. 
```shell
adk web  # run this from the sample_agent directory
```
There are other options as well to run your agent  
`adk run` – Interact with your agent directly from the terminal, without opening a web browser.  
`adk api_server` – runs your agent as a REST API service. Other applications acn send requests to your agent over HTTP  
It is also possible to use the agent in a progammatic way directly from your python code for eample from your Jupyter notebook, data processing pipeline etc.

We will stck to `adk web` for now. With this, you should see the below output in the console
```shell
INFO:     Started server process
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
```
Open the link in a browser and you can interact with your agent with this interface. You may need to select your agent from the left side dropdown.

#### **What you have seen so far**
`Agent = model + tools + orchestration`  
`model` is an LLM which acts as the brain of your agent  
`tools` are unctions that your agent can call to take actions. These bridge “knowing” to “doing”  
`orchestration` manages the whole process of *perceive → think → act → check → repeat*



## **Our Use Case : Automated PR Reviewer**
We would be building a PR review agent using Google ADK. Instead of a single bot giving a generic response, we will create multiple specialized agents working together and reviewing the code from different angles. Its like a code `Review Board` of security specialist, performance experts, documentaion and best practices experts.

#### **The Orchestrator Agent**
The orchestrator agent which integrate the other specialized sub-agentsand the Github MCP tools.
```python
import os

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPConnectionParams

from .sub_agents.code_logic import code_logic_agent
from .sub_agents.code_quality import code_quality_agent
from .sub_agents.security_specialist import security_specialist_agent

GITHUB_TOKEN = os.environ['GITHUB_TOKEN']

root_agent = Agent(
    model="gemini-3-flash-preview",
    name="github_expert_agent",
    description="Main entry point for Git/GitHub tasks and PR reviews.",
    instruction="""
    You are the Lead Maintainer. 
    1. For PR reviews, fetch the diff using your tools.
    2. Delegate the diff to 'security_specialist_agent','code_quality_agent' and 'code_logic_agent' for specific checks.
    3. Consolidate their feedback and use your tools to post a final, combined review.
    """,
    sub_agents=[security_specialist_agent, code_quality_agent, code_logic_agent],
    tools=[
        McpToolset(
            connection_params=StreamableHTTPConnectionParams(
                url="https://api.githubcopilot.com/mcp",
                headers={
                    "Authorization": f"Bearer {GITHUB_TOKEN}",
                    "X-MCP-Toolsets": "all",
                    "Accept": "application/json, text/event-stream"
                },
            ),
        )
    ],
)

```
### Security Specialist Agent
The security specialist agent focusing on the security aspects of the code.
```python
from google.adk.agents import Agent

security_specialist_agent = Agent(
    model="gemini-3-flash-preview",
    name="security_specialist",
    description="Handles deep security analysis, vulnerability detection, and secret scanning.",
    instruction="Scan the provided diff for security risks. Provide specific file and line numbers for issues."
)

```
### Code Quality Expert Agent
The code quality agent checking the coding best practices etc.
```python
from google.adk.agents import Agent

code_quality_agent = Agent(
    model="gemini-3-flash-preview",
    name="code_quality_expert",
    description="Analyzes code quality, coding best practices, and code documentation related problems.",
    instruction="Scan the provided diff for code quality, coding best practices, and code documentation related problems."
)

```
### The Code Logic Agent
The expert coder checking code logic, performance bottleneck etc.
```python
from google.adk.agents import Agent

code_logic_agent = Agent(
    model="gemini-3-flash-preview",
    name="code_logic_expert",
    description="Analyzes code logic, performance, and potential runtime errors.",
    instruction="Review the code for logical correctness and performance bottlenecks."
)

```

### Putting it all together
#### run from terminal
```shell
#Step 1
adk run github_agent
```
#### run as API
```shell
#Step 1
adk api_server github_agent

#Step 2
curl -X POST http://localhost:8000/
your-endpoint -H "Content-Type: application/json" -d \
'{"message": "is there any pending PR in the rphukan/agentic-ai-samples repository"}'
```
### Future Enhancements

## Thank you