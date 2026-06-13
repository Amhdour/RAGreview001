# User Prompt Handling

| User prompt path | File/path | Line reference if available | Input source | Destination | Security relevance | Missing evidence | Evidence label |
| ---------------- | --------- | --------------------------- | ------------ | ----------- | ------------------ | ---------------- | -------------- |
| Chat request intake | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | process_message.py:660-823 | End-user chat text and attachments | Chat message creation and history chain | User input becomes part of downstream LLM history | OBSERVATION | Runtime injection validation not proven |
| Message history conversion | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | chat_utils.py:163-260; llm_step.py:844-1002 | Prior user/assistant/tool messages | LLM input message list | History is flattened and reordered for model consumption | OBSERVATION | No adversarial history test evidence |
| User query to search | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | process_message.py:660-823; search_tool.py:539-745 | User query and search params | Search queries and filters | User text can influence retrieval scope | OBSERVATION | No runtime prompt-injection guard proven |
| User prompt reminders / custom prompts | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | llm_loop.py:303-602; chat_backend.py:136-149 | Persona task prompt and user-visible reminders | System/user message stream | User-facing prompt fragments are inserted alongside system content | OBSERVATION | No hierarchy enforcement evidence |
| Image and file payload handling | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | llm_step.py:898-1002; chat_utils.py:940-989 | Image/file-bearing user messages | Multimodal LLM input / file context | Non-text content is preserved in model input | OBSERVATION | No prompt-injection-specific image/file validation |
| Search query normalization | backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598 | prompts/search_prompts.py:15-79; process_message.py:501+ | Search terms and filters | Search prompt / search pipeline | User text may be rephrased before retrieval | OBSERVATION | No evidence of malicious-query filtering |

## Missing evidence
- No runtime prompt-injection detection on user text was identified.
- No explicit user-input policy engine was identified in the reviewed sources.

## Notes
- User prompts are handled as ordinary input to chat, retrieval, and tool flows.
- Source evidence shows message conversion and query routing, not prompt-injection resistance.
