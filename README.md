# OpenAI AI Chat Desktop App

A desktop GUI application for interacting with OpenAI family of language models. Built with Python and `tkinter`, this app provides a robust and user-friendly interface for managing multiple chat conversations with advanced features like reasoning effort control and precise token tracking.

## Description

This application allows users to chat with various OpenAI models through a clean, resizable, three-panel interface. It's designed to be a powerful tool for developers, writers, and anyone looking to explore the capabilities of OpenAI large language models locally. You can manage separate conversations, each with its own context, API key, model, and reasoning settings, making it easy to organize different projects and experiments.

## Features

* **Modern Dark Theme**: A sleek, easy-on-the-eyes dark interface for comfortable use.
* **Multi-Conversation Management**: Create and switch between multiple, named conversations. Each conversation maintains its own independent chat history.
* **Flexible Configuration**: Assign a different OpenAI model and API key to each conversation.
* **Reasoning Effort Control** *(New in v0.6)*: 
    * Configure reasoning effort levels (low/medium/high) for compatible models.
    * Currently supports models in the gpt-5 family.
    * Per-conversation reasoning settings with live UI updates.
* **Dynamic Model Loading**: Automatically fetches and displays a list of available OpenAI models directly from the API, ensuring you always have access to the latest versions.
* **API Key Management**: For convenience, the app can read your OpenAI API key from a local `OpenAI_API_key.txt` file, or you can enter it directly in the UI.
* **Enhanced Token Tracking** *(Improved in v0.5)*:
    * Precise token counting using `tiktoken` encoding.
    * View the total token count for the current conversation's context.
    * See the token count for any selected message in the history.
    * Get an on-demand token count for your prompt before sending it.
    * Automatic token count updates after each message.
* **Advanced Conversation Threading** *(New in v0.5)*:
    * Improved message continuity with OpenAI's conversation threading.
    * Better context preservation across multiple exchanges.
    * Robust reply extraction with fallback parsing.
* **User-Friendly Interface**:
    * A resizable three-panel layout (Message History, Message Content, Prompt Editor).
    * The leftmost Message History panel shows the list of all previous messages in the current conversation. Each message can be easily selected and viewed in the Message Content panel.
    * A "Waiting for response..." indicator prevents the UI from appearing frozen during API calls.
    * Copy message content to the clipboard with a single click.
    * Improved conversation switching and UI synchronization *(Enhanced in v0.6)*.
* **Windows Taskbar Notifications**: For Windows users, the app icon will flash in the taskbar when a new message is received while the window is not in focus (requires `pywin32`).

## Requirements

* Python 3.x
* `openai` (latest version for enhanced features)
* `tiktoken` *(New dependency in v0.5)* - for accurate token counting
* `pywin32` (Optional, for taskbar notifications on Windows)

## Installation and Usage

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repository-name.git](https://github.com/your-username/your-repository-name.git)
    cd your-repository-name
    ```

2.  **Install the required packages:**
    It is recommended to use a virtual environment.
    ```bash
    # Create and activate a virtual environment (optional but recommended)
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

    # Install dependencies
    pip install openai tiktoken pywin32
    ```

3.  **(Optional) Set up your API Key file:**
    Create a text file named `OpenAI_API_key.txt` in the same directory as the script and paste your OpenAI API key inside. This allows the app to automatically load your key on startup.

4.  **Run the application:**
    ```bash
    python openai_chat_app.py
    ```

## Usage Instructions

### Getting Started
1. **Launch the app** and click "New Conversation" to create your first conversation.
2. **Enter your API key** (or the app will auto-load from `OpenAI_API_key.txt` if available).
3. **Select a model** by clicking "Load Models" to fetch available options from OpenAI.
4. **Choose reasoning effort** (for compatible models like gpt-5) - options are low, medium, or high.
5. **Name your conversation** for easy identification.
6. **Start chatting** by typing in the prompt area and clicking "Send" or pressing Ctrl+Enter.

### Advanced Features
* **Multiple Conversations**: Create separate conversations for different topics or projects.
* **Token Management**: Monitor token usage for both individual messages and entire conversations.
* **Reasoning Control**: Adjust reasoning effort for models that support it to balance response quality and processing time.
* **Message History**: Click on any previous message to view its full content and token count.

## Troubleshooting

* **"Models not loading"**: Ensure your API key is valid and has proper permissions.
* **"Reasoning controls disabled"**: Reasoning effort is only available for compatible models (currently gpt-5 family).
* **"Taskbar flashing not working"**: Install `pywin32` or run on Windows for this feature.

## License


All content and source code for this application are subject to the terms of the MIT License.
