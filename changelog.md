# Changelog — OpenAI Interface App

## Version 0.6.1

### Improved
- __Reasoning Effort selector UX enhancement__:
  - Reasoning effort combobox now displays `(unavailable)` when disabled for incompatible models.
  - Both main window and New Conversation dialog show clear feedback when reasoning controls aren't available.
  - Default state shows `(unavailable)` at app startup and when no compatible model is selected.
  - Improved user experience with intuitive visual feedback for feature availability.

### Fixed
- __Combobox values synchronization__:
  - Added `(unavailable)` to reasoning effort combobox values list for proper UI rendering.
  - Ensures consistent display behavior across all reasoning effort selector states.

## Version 0.6

### Added
- __Reasoning Effort selector__ in `openai_chat_app.py`:
  - New combobox in both the New Conversation dialog and the main window controls with values `low | medium | high`.
  - Default is `medium`. Controls are enabled only for compatible models (see Notes).
- __Per-conversation reasoning setting__:
  - `OpenAIChatSession.reasoning_effort` attribute stores the selected effort for each conversation.
  - API calls include `reasoning={"effort": <value>}` when compatible.

### Changed
- __Dialog result now includes reasoning effort__:
  - `NewConversationDialog` returns `(api_key, model_name, conversation_name, effort)`; effort is applied to the new session if compatible.
- __UI synchronization__:
  - `AIChatApp` updates the reasoning combobox when the active conversation changes and applies user changes live to the session.

### Fixed
- __Recursion bug in `AIChatApp._on_active_conversation_change()`__ eliminated and the method now safely updates related UI.
- __Reasoning controls wiring__:
  - Implemented `AIChatApp._update_reasoning_controls()` and `AIChatApp._on_reasoning_effort_change()`.
  - Implemented `AIChatApp._on_conversation_combobox_select()` for switching active conversations from the combobox.
- __Duplicate methods__:
  - Removed an obsolete duplicate of `_add_new_conversation`.
- __Missing combobox refresh__:
  - Implemented `AIChatApp._update_conversation_combobox()` to refresh the conversation list after creating a new one.

### Notes
- __Compatibility rule__: reasoning effort is enabled for models whose name starts with `gpt-5` (via `OpenAIChatSession._is_reasoning_compatible_model`).
- __Defaults__: when unset/invalid, effort falls back to `medium`; controls are disabled for incompatible models.
- __API requests__: the reasoning parameter is respected in both normal and retry code paths.

## Version 0.5

### Added
- __OpenAI client initialization and wrappers__ in [openai_chat_app.py](cci:7://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:0:0-0:0):
  - `OpenAIChatSession.__init__` now creates an [OpenAI](cci:2://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:54:0-222:39) client.
  - [_ClientWrapper](cci:2://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:42:0-51:66), [_ModelsWrapper](cci:2://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:27:0-39:39), [_TokenCountResult](cci:2://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:22:0-24:40) provide `client.models.count_tokens(...)` via `tiktoken`.
- __Token counting utilities__:
  - [_get_encoding_for_model()](cci:1://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:188:4-202:55) with fallbacks (`o200k_base` → `cl100k_base`).
  - `OpenAIChatSession.update_token_count(history)` to compute “Tokens in context”.

### Changed
- __Message sending and conversation threading__:
  - `OpenAIChatSession.send_message_to_OpenAI_API(prompt, history=None)` implemented using `client.responses.create(...)`, `store=True`, and `previous_response_id` threading.
  - Robust reply extraction using `response.output_text` with fallback parsing.
  - Role mapping for history replay (`'model'` → `'assistant'`).
- __Conversation integration__:
  - `Conversation.send_message()` passes `history=self.chat_history` and updates total tokens after each send.
- __Model loading__:
  - `NewConversationDialog._load_models()` fetches models via [OpenAI(api_key).models.list()](cci:2://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:54:0-222:39) and populates the combobox.

### Fixed
- __Multi-turn 400 error (“previous_response_not_found”)__:
  - Set `store=True` to persist responses for `previous_response_id` references.
  - Added retry fallback: on missing previous response, resend full history + prompt without `previous_response_id`.

### Notes
- __GUI unchanged__; all integration honors existing widgets and flows.
- __Token counts__ are local approximations using `tiktoken` but consistent across:
  - Selected message tokens ([_on_treeview_message_select()](cci:1://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:820:4-858:66)).
  - Prompt tokens ([_update_prompt_token_count()](cci:1://file:///d:/Programming/Python/Windsurf/OpenAI_Interface_App/openai_chat_app.py:1038:4-1066:60)).
  - Total tokens in context (top bar via `OpenAIChatSession.token_count`).

## Version 0.4

Initial commit.