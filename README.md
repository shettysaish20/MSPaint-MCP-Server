# Model Context Protocol (MCP) MSPaint App Automation

This project demonstrates how to automate interactions with a legacy Windows application (MSPaint) using the Model Context Protocol (MCP). It leverages `pywinauto` to control the Paint application and `fastmcp` to define tools that can be called by an AI agent. The AI agent, powered by Google's Gemini model, uses these tools to perform tasks such as drawing rectangles and adding text to the Paint canvas.

## Table of Contents

- [Introduction](#introduction)
- [Model Context Protocol (MCP)](#model-context-protocol-mcp)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Setup](#setup)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Key Components](#key-components)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project showcases the automation of MSPaint using an AI agent. The agent can open Paint, draw rectangles, and add text, all driven by natural language instructions. This is achieved through the Model Context Protocol (MCP), which allows the AI agent to call specific functions (tools) defined in the Python code.

## Model Context Protocol (MCP)

The Model Context Protocol (MCP) is a framework that enables AI models to interact with external tools and resources. It provides a standardized way for models to call functions, retrieve data, and perform actions in the real world. In this project, MCP is used to expose Paint automation functions as tools that the AI agent can use.

## Project Structure

```
├── MSPaint-MCP-Server/
│ ├── mcp_server.py # Defines the MCP server with tools for Paint automation 
│ ├── mcp_client.py # Defines the MCP client that interacts with the server and AI model 
│ ├── requirements.txt # Lists the project dependencies 
│ └── .env # Stores the Gemini API key 
├── README.md # This file
```

## Requirements

- Python 3.11+
- Conda (recommended for environment management)
- Google Gemini API key
- pywin32
- pywinauto
- fastmcp
- python-dotenv
- google-genai

## Setup

1.  **Create a Conda environment:**

    ```bash
    conda create -n eagenv python=3.11
    conda activate eagenv
    ```

2.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Set up the Gemini API key:**

    -   Create a `.env` file in the directory.
    -   Add your Gemini API key to the `.env` file:

        ```
        GEMINI_API_KEY=YOUR_API_KEY
        ```

## Usage

1.  **Run the MCP client:**

    ```bash
    python mcp_paint_app/mcp_client.py
    ```

    This will start the MCP client, which connects to the MCP server, initializes the AI agent, and begins the automation process.

## How It Works

1.  **MCP Server (`mcp_server.py`):**
    -   Defines the tools for interacting with MSPaint (e.g., `open_paint`, `draw_rectangle`, `add_text_in_paint`).
    -   Uses `pywinauto` to control the MSPaint application.
    -   Exposes these tools via the `fastmcp` library.

2.  **MCP Client (`mcp_client.py`):**
    -   Connects to the MCP server.
    -   Uses the Google Gemini model to generate instructions.
    -   Parses the model's output to determine which tool to call.
    -   Calls the appropriate tool on the MCP server.
    -   Handles the response from the tool and feeds it back to the model.

3.  **AI Agent (Google Gemini):**
    -   Receives a query (e.g., "Return the sum of first 20 Fibonacci numbers.").
    -   Uses the available tools (defined in the system prompt) to solve the problem.
    -   Generates function calls (e.g., `FUNCTION_CALL: fibonacci_numbers|20`) to use the tools.
    -   Provides a final answer (e.g., `FINAL_ANSWER: 6765`) and uses Paint to display the result.

## Key Components

-   **`mcp_server.py`:** Contains the core logic for automating MSPaint. The `open_paint`, `draw_rectangle`, and `add_text_in_paint` functions are the key tools used by the AI agent.
-   **`mcp_client.py`:** Manages the interaction between the AI agent and the MCP server. It sets up the system prompt, calls the tools, and handles the responses.
-   **`requirements.txt`:** Lists all the necessary Python packages for the project.
-   **.env:** Stores the Google Gemini API key.

## Troubleshooting

-   **Permission Issues:** If you encounter permission issues, try running the scripts as an administrator.
-   **Coordinate Issues:** The coordinates used for clicking in MSPaint may need to be adjusted based on your screen resolution and window size. Use the debugging print statements in the code to identify the correct coordinates.
-   **Tool Selection Issues:** If the AI agent is not selecting the correct tools, review the system prompt and ensure that the tool descriptions are accurate.
-   **API Key Issues:** Ensure that your Gemini API key is correctly set in the `.env` file.

## Contributing

Contributions are welcome! Please submit a pull request with your changes.

## License

[MIT License](LICENSE)