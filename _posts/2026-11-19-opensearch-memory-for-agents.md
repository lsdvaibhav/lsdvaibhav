---
layout: post
title: "Amazon OpenSearch Memory is generally available"
date: 2026-11-19 09:00:00 +0530
summary: "AWS launched a serverless memory store so agents can recall customer context across sessions without sending the full transcript to the model."
tags:
  - agents
  - customer-experience
  - rag
references:
  - title: "Introducing Amazon OpenSearch Memory: Persistent memory for AI agents"
    url: "https://aws.amazon.com/blogs/big-data/introducing-amazon-opensearch-memory-persistent-memory-for-ai-agents/"
  - title: "What is Amazon OpenSearch Memory? — Amazon OpenSearch Service Developer Guide"
    url: "https://docs.aws.amazon.com/opensearch-service/latest/developerguide/memory.html"
---

On 18 November 2026, AWS made Amazon OpenSearch Memory generally available. Agents write each turn as an event, and the service extracts facts and session summaries in the background, then returns them with hybrid search before the next reply.

That is a practical pattern for customer-experience agents. A support assistant can pick up an open case, a preference, or a promise made last session without putting the whole transcript back in the prompt. In AWS's LongMemEval write-up, this workflow used about 13,500 input tokens per question against roughly 167,000 for the full history, with answer accuracy of 93.0% compared with 95.2%. Connections include the AWS SDK and an MCP server, so it can sit beside the tool-using agents already running in production.
