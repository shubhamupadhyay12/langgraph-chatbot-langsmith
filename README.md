# LangGraph Chatbot with LangSmith Tracing

Several versions of a chatbot built with **LangGraph** and **LangChain**. Each version adds something to the one before it: conversation memory, tool calling, conditional routing, and LangSmith tracing so every run can be inspected step by step.

## What it does

- Runs a conversation as a LangGraph graph, where each step (call the model, run a tool, decide what happens next) is a node
- Keeps conversation state and chat history across turns
- Calls tools when the model asks for them (live calculations, search, external APIs) and feeds the results back into the conversation
- Routes between nodes with conditional edges
- Sends every run to LangSmith, so you can see each node, tool call, token count, and latency

## How a message flows

1. The user sends a message and it is added to the graph state.
2. The graph passes the conversation to the language model.
3. The model either answers directly or requests a tool.
4. If a tool is requested, it runs and the result goes back to the model.
5. The updated state is saved and the final answer is returned.

## Tech stack

Python, LangGraph, LangChain, LangSmith, python-dotenv

## Run it

```bash
git clone https://github.com/shubhamupadhyay12/langgraph-chatbot-langsmith.git
cd langgraph-chatbot-langsmith

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Create a `.env` file (never commit it):

```env
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langsmith_api_key
LANGCHAIN_PROJECT=langgraph-chatbot
OPENAI_API_KEY=your_model_provider_key
```

Each file in the repo is a standalone version of the chatbot. Run any one directly, for example:

```bash
python langgraph_database_backend.py
```

## Tracing with LangSmith

With tracing on, each run shows up in your LangSmith project. From there you can open a run and check the inputs and outputs of every node, which tool was called with what arguments, how long each step took, and how many tokens were used. This was the main way I debugged multi-step runs.

## Author

Shubham Upadhyay · [GitHub](https://github.com/shubhamupadhyay12) · [LinkedIn](https://www.linkedin.com/in/shubhamupadhyay25)

**Shubham Upadhyay**

## License

This project is available under the license included in the repository.
