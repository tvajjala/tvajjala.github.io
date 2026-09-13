---
layout: post
title: "LangChain and LangGraph Frameworks"
date: 2026-09-13
description: When to use LangChain's agent abstractions and LangGraph's stateful orchestration.
---

> LangChain helps assemble models and tools quickly. LangGraph gives the workflow explicit state, routing, persistence, and control.

##### LangChain: the application layer

LangChain provides model integrations, tool definitions, message handling, retrieval components, and prebuilt agent patterns. It is a strong fit when the application has a familiar tool-calling loop and the primary goal is to connect an LLM to useful data and actions quickly.

A typical LangChain flow looks like this:

1. Receive a user request.
2. Give the model a set of well-defined tools.
3. Let the model choose a tool when it needs information or an action.
4. Return the tool result to the model and produce a final answer.

This is often enough for a chat assistant, a retrieval workflow, or a focused automation.

##### LangGraph: the orchestration layer

LangGraph is a lower-level runtime for long-running, stateful workflows. A graph has nodes that perform work, edges that determine the next step, and shared state that carries information between steps.

Use LangGraph when the workflow needs more control than a linear agent loop:

* **Conditional routing** - send a request to retrieval, analysis, or escalation based on state.
* **Durable execution** - checkpoint progress so a run can resume after a failure or a long wait.
* **Human-in-the-loop review** - pause before an action, gather approval or edits, then resume.
* **Parallel or multi-step work** - coordinate independent investigations and combine their results.
* **Observability** - inspect state transitions and diagnose why a workflow reached a decision.

##### Choosing between them

| Need | Recommended starting point |
| --- | --- |
| A model, a few tools, and a standard agent loop | LangChain |
| A stateful workflow with explicit branches and retries | LangGraph |
| A production operation that must pause for approval | LangGraph with persistence |
| A new application that may become more complex | Start with LangChain, introduce LangGraph when state and control flow become first-class concerns |

LangChain and LangGraph are complementary rather than competing. LangChain components can supply models, tools, and retrievers inside a LangGraph workflow. The important design decision is to make side effects explicit: validate inputs, separate planning from execution, and require approval for irreversible actions.

##### Reference

* [LangChain overview](https://docs.langchain.com/oss/python/langchain/overview)
* [LangGraph overview](https://docs.langchain.com/oss/python/langgraph/overview)
* [LangGraph persistence](https://docs.langchain.com/oss/python/langgraph/persistence)
