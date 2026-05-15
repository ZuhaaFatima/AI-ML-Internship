# Task 4: General Health Query Chatbot (Prompt Engineering Based)

---

## Task Objective
Build a chatbot that answers general health-related questions using a Large Language Model (LLM).
The chatbot uses prompt engineering to make responses friendly, clear, and safe.
A safety filter is also added to handle harmful or emergency queries responsibly.

---

## Dataset Used
No external dataset was used for this task.
The model is a pre-trained LLM accessed via the Hugging Face Inference API.
It was tested on the following example queries as specified in the task:

| Query | Type |
|---|---|
| "What causes a sore throat?" | Required example |
| "Is paracetamol safe for children?" | Required example |
| "How can I manage stress better?" | Bonus test |
| "What are the symptoms of dehydration?" | Bonus test |
| "I have severe chest pain" | Emergency safety test |

---

## Models Applied
| Model | Provider | Cost |
|---|---|---|
| `meta-llama/Llama-3.1-8B-Instruct:cerebras` | Hugging Face Inference Router | Free |

- **API Used**: Hugging Face OpenAI-compatible router (`https://router.huggingface.co/v1`)
- **Library**: `openai` Python SDK pointed at Hugging Face router
- **Prompt Engineering**: System prompt with persona assignment, 7 safety rules, tone control, and length control

---

## Key Results and Findings

- **Prompt engineering works without fine-tuning** — writing a detailed system prompt
  with a persona, safety rules, and tone instructions was enough to make the model
  behave like a responsible health assistant without any model training

- **Two-layer safety is more reliable than one** — combining an emergency keyword
  filter (pre-API) with system prompt guardrails (inside the LLM) gave better
  protection than using either method alone

- **Conversation history enables smarter replies** — storing previous messages and
  sending them with every request allowed the chatbot to understand follow-up
  questions in context

- **Hugging Face free tier is sufficient** — the free Llama-3.1-8B model via
  Hugging Face produced accurate, helpful, and appropriately cautious responses
  for all tested health queries

- **Model name format matters** — the new Hugging Face router requires a
  `:provider` suffix in the model name (e.g. `model-name:cerebras`),
  otherwise the request fails with a 400 error

---

## How to Run

1. Get a free token from https://huggingface.co/settings/tokens
   (Fine-grained token with Make calls to Inference Providers permission)
2. Paste your token in Step 3 of the notebook
3. Run `Kernel → Restart & Run All`

---

## Disclaimer
This chatbot provides general health information only.
It is not a substitute for professional medical advice.
Always consult a qualified doctor for personal health decisions.
