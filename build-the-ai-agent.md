

# 🚀 AI Agent Workflow --- Motivational Response Generator
------------------------------------------------------

This scenario receives user emotional input via webhook, analyzes it using multiple AI stages, selects a motivational persona, crafts a personalized message, and responds --- all autonomously.

* * * * *

## Image of the Ideal Workflow: 

![image](https://github.com/user-attachments/assets/ad7ce100-0133-4fe1-96f0-25c60d578aa8)


### 🧠 Overview

| Step | Module | Purpose |
| --- | --- | --- |
| 1 | `gateway:CustomWebHook` | Trigger on user emotional input |
| 2 | `gemini-ai:createACompletionGeminiPro` | Detect user mood using LLM |
| 8 | `gemini-ai:createACompletionGeminiPro` | Select motivational persona from preset list |
| 9 | `gemini-ai:createACompletionGeminiPro` | Summarize user's issue in one sentence |
| 10 | `gemini-ai:createACompletionGeminiPro` | Craft motivational reply using selected persona |
| 11 | `gateway:WebhookRespond` | Send final message back to user |

* * * * *

### 📥 Webhook Trigger

```
{
  "hook": 2472283,
  "label": "MyMotivationProject",
  "maxResults": 1
}

```

This module receives user input containing emotional text and initiates the scenario.

* * * * *

### 🤖 Gemini AI Stage 1: Mood Detection

**Prompt:**

> You are a smart AI that can accurately detect the mood...\
> Output **only one word** --- the mood.

**Output Example:**

```
anxious

```

* * * * *

### 🎭 Gemini AI Stage 2: Persona Selection

**Prompt:**

> Based on user's input, choose one best motivational persona from this list:\
> David Goggins, Chris Williamson, Jordan Peterson, Jocko Willink, Kobe Bryant, Mel Robbins, Marie Forleo

**Output Example:**

```
Chris Williamson

```

* * * * *

### 🧵 Gemini AI Stage 3: Emotional Summary

**Prompt:**

> Read the message and **summarize what the user is going through** in **one sentence**.

**Output Example:**

```
The user feels like they've lost direction despite working hard.

```

* * * * *

### 💬 Gemini AI Stage 4: Craft Response

**Prompt:**

> Using the selected persona and tone, validate the user's feelings, insert a quote, and respond in 5--6 raw motivational lines.

**Output Format:**

```
[Comforting sentence]
As [Persona] once said, "quote."
[line 1]
[line 2]
...
[line 6]

```

* * * * *

### 📤 Webhook Response

```
{
  "status": "200",
  "body": "{{10.result}}"
}

```

Sends the final crafted message back to the originating platform or user interface.



## Entire flow:

```
{
  "name": "Integration Webhooks",
  "flow": [
    {
      "id": 1,
      "module": "gateway:CustomWebHook",
      "parameters": {
        "hook": "<REDACTED>",
        "maxResults": 1
      }
    },
    {
      "id": 2,
      "module": "gemini-ai:createACompletionGeminiPro",
      "parameters": {
        "__IMTCONN__": "<REDACTED>"
      },
      "mapper": {
        "model": "gemma-3n-e4b-it",
        "contents": [
          {
            "role": "user",
            "parts": [
              {
                "type": "text",
                "text": "Detect mood from user input"
              }
            ]
          }
        ]
      }
    },
    {
      "id": 8,
      "module": "gemini-ai:createACompletionGeminiPro",
      "parameters": {
        "__IMTCONN__": "<REDACTED>"
      },
      "mapper": {
        "model": "gemma-3n-e4b-it",
        "contents": [
          {
            "role": "user",
            "parts": [
              {
                "type": "text",
                "text": "Choose best motivational persona"
              }
            ]
          }
        ]
      }
    },
    {
      "id": 9,
      "module": "gemini-ai:createACompletionGeminiPro",
      "parameters": {
        "__IMTCONN__": "<REDACTED>"
      },
      "mapper": {
        "model": "gemma-3n-e4b-it",
        "contents": [
          {
            "role": "user",
            "parts": [
              {
                "type": "text",
                "text": "Summarize user's situation in one sentence"
              }
            ]
          }
        ]
      }
    },
    {
      "id": 10,
      "module": "gemini-ai:createACompletionGeminiPro",
      "parameters": {
        "__IMTCONN__": "<REDACTED>"
      },
      "mapper": {
        "model": "gemma-3n-e4b-it",
        "contents": [
          {
            "role": "user",
            "parts": [
              {
                "type": "text",
                "text": "Generate motivational reply with tone and quote"
              }
            ]
          }
        ]
      }
    },
    {
      "id": 11,
      "module": "gateway:WebhookRespond",
      "mapper": {
        "status": "200",
        "body": "{{10.result}}",
        "headers": []
      }
    }
  ],
  "metadata": {
    "version": 1,
    "scenario": {
      "autoCommit": true
    }
  }
}

```
