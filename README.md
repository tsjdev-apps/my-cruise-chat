# My Cruise Chat

An Blazor (.NET 9) AI chat application tailored to answer questions about a specific winter cruise on the MSC Euribia (January 2024).  

It combines:
- Streaming AI responses
- A system-enforced domain scope (cruise-only Q&A)
- A semantic search tool with structured `<result>` output
- Automatic follow‑up suggestions
- Inline citations emitted as `<citation ...>` XML tags at the end of each AI response

---

## Features

| Feature | Description |
|---------|-------------|
| Domain-restricted assistant | System prompt prevents off-topic answers. |
| Streaming responses | Tokens stream into the UI (`TextContent` accumulation). |
| Semantic search tool | Invoked via `chatOptions.Tools` using `AIFunctionFactory.Create(SearchAsync)`. |
| XML citation format | `<citation filename='...' page_number='...'>short quote</citation>` appended automatically when search results are used. |
| Search results format | Tool returns `<result filename="..." page_number="...">...</result>` elements (max 5). |
| Conversation reset | Via `ChatHeader` invoking `ResetConversationAsync()`. |
| Suggestions component | Updates after each completed assistant reply. |
| User focus management | Input refocus after send/reset. |
| Cancellation-safe streaming | Partial assistant answers preserved if cancelled. |

---

## Tech Stack

- Blazor
- .NET 9 / C# 13 features
- Dependency Injection for `IChatClient` and `SemanticSearch`
- Pluggable tool model for function calling

---

## System Prompt Logic (Chat.razor)

The assistant is constrained to:
1. Only answer cruise-related questions derived from retrieved content.
2. Use semantic search when answering.
3. Emit `<citation ...>` tags (each with:
   - filename
   - page_number
   - a max 5-word exact quote from the source)

The UI does not display explanatory boilerplate about citations—only the tags.

---

## Disclaimer

AI responses are constrained but not guaranteed to be perfect. Validate critical information before reliance.

---

Happy cruising & coding!
