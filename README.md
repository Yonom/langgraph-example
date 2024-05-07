# `langgraph-api` Example

This is an example of how to use the `langgraph-api` to stand up a REST API for your custom LangGraph StateGraph. This API can be used to interact with your StateGraph from any programming language that can make HTTP requests. It has the following features:

- saved assistants
- saved threads, with state/conversation history
- human in the loop endpoints (interrupt, get thread state, update thread state, get history of past thread states)
- streaming runs (with multiple stream formats, including token-by-token messages, state values and node updates)
- background runs (with api for checking status and events, and support for completion webhooks)

We've designed it as a robust server you can run in production at high scale, and also easily test locally.

## Getting started

First, install the `langgraph-cli` package:

```bash
pip install langgraph-cli
```

Then, create a `langgraph.json` file with your configuration. You can declare local and external python dependencies (which will be installed with `pip`), env vars (or an env file) and the path to your StateGraph. You can expose multiple StateGraphs in the same API server by providing multiple paths. Here's an example:

```json
{
  "dependencies": [
    "langchain_community",
    "langchain_anthropic",
    "langchain_openai",
    "wikipedia",
    "scikit-learn",
    "./graphs"
  ],
  "graphs": {
    "agent": "./graphs/agent.py:graph"
  },
  "env": ".env"
}
```

In the `graphs` mapping, the key is the `graph_id` and the value is the path to the StateGraph. The `graph_id` is used in the API to refer to the StateGraph.

The `env` field can be a path to an env file or a dictionary of environment variables. These environment variables will be available to your LangGraph code.

Then, run the following command to start the API server:

```bash
langgraph up
```

This will start the API server on `http://localhost:8123`. You can now interact with your StateGraph using the API or SDK.

If you're calling this API from Python, you might want to use the `langgraph-sdk` package, which provides a Python client for this API.

## API Reference

The API reference is available at `http://localhost:8123/docs`.