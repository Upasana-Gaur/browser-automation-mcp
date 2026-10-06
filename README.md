# 🤖 AI-Powered Browser Automation MCP Server

 A **Model Context Protocol (MCP) server** built with **Python, Playwright, and FastMCP** that provides browser automation capabilities as structured tools for AI agents and LLMs.

 The server allows AI systems to **open web pages, navigate websites, interact with page elements, fill forms, click buttons, handle checkboxes and dropdowns, simulate keyboard actions, scroll pages, and inspect web-page content** through MCP tools.

---

 ## 🚀 Tech Stack

 - **Python**
- **Playwright (Async API)**
- **FastMCP**
- **Pydantic**

---

 ## ✨ Features

 ### 🌐 Page Management

 - Open new browser pages with a unique `pageId`
- Navigate to different URLs
- Move to the previous or next page
- Reload the current page
- Close browser pages
- Maintain multiple pages using session-based page IDs

 ### ✍️ Smart Form Filling

 Fill input fields using different locator strategies:

 - Text
- Label
- Placeholder
- Title
- ARIA role

 This allows automation tools to interact with web forms without relying only on CSS selectors or XPath.

 ### 🖱️ Smart Clicking

 Click web elements using:

 - Text
- Label
- Placeholder
- Title
- ARIA role
- X/Y coordinates

 Supports:

 - Single click
- Double click
- Mouse buttons
- Keyboard modifiers such as `Alt`, `Control`, `Meta`, and `Shift`

 ### ☑️ Checkbox & Radio Button Handling

 Interact with checkbox and radio elements using:

 - Text
- Label
- Title
- ARIA role

 Supports selecting and changing the checked state of elements.

 ### 📋 Dropdown Selection

 Select options from `<select>` elements using:

 - Text
- Label
- Placeholder
- Title
- ARIA role

 ### ⌨️ Keyboard Automation

 Simulate keyboard actions and shortcuts such as:

```
Enter
Tab
Escape
Control+A
Control+C
Control+V
Shift+Tab
```

 ### 📜 Page Scrolling

 Scroll web pages horizontally and vertically using configurable X and Y scroll distances.

 ### 🔍 Page Summarizer

 The server provides a compact, structured summary of the current page that can be used by an AI agent to understand the page before performing actions.

 The summary can include:

 - Page metadata
- Headings
- Buttons
- Links
- Input fields
- Checkboxes
- Interactive elements
- Tabs
- Menus
- Sliders
- Tree items
- Dialogs
- Alerts
- Forms
- Text preview
- Element counts
- Useful locator information

 This helps reduce the amount of raw webpage content that needs to be passed to an LLM.

---

 ## 🛠️ Installation

 ### Prerequisites

 Make sure the following are installed:

 - **Python 3.9 or later**
- **Google Chrome**
- **pip**

 You can verify Python and Chrome installation before setting up the project.

```
python --version
```

---

 ## 📦 Setup

 ### 1\. Clone the Repository

```
git clone <your-repo-url>
cd browser-automation-mcp
```

 ### 2\. Install Python Dependencies

```
pip install mcp[cli] playwright pydantic
```

 ### 3\. Install Playwright Chrome Support

```
playwright install chrome
```

---

 ## ▶️ Usage

 ### Run the MCP Server

 Start the MCP server using:

```
python script.py
```

 The server will start and wait for MCP client requests.

 The browser is launched using Chrome with the browser window visible, allowing browser actions to be observed while the automation is running.

---

 ## 🔌 Connect to an MCP Client

 This server can be connected to an MCP-compatible client such as **Claude Desktop**.

 For example, add the server to your MCP client configuration:

```
{
  "mcpServers": {
    "BrowserAutomation": {
      "command": "python",
      "args": [
        "/path/to/script.py"
      ]
    }
  }
}
```

 Replace:

```
/path/to/script.py
```

 with the absolute path to your project's `script.py`.

 ### Example

 On Windows, the configuration can look like:

```
{
  "mcpServers": {
    "BrowserAutomation": {
      "command": "python",
      "args": [
        "C:\\path\\to\\browser-automation-mcp\\script.py"
      ]
    }
  }
}
```

 After adding the configuration, restart the MCP client so it can load the server.

---

 ## 🧰 Available MCP Tools

 The server exposes browser automation functions through MCP tools.

 ### Page Management

 | Tool | Purpose |
| --- | --- |
| `open_page` | Open a new webpage |
| `previous_page` | Navigate to the previous page |
| `next_page` | Navigate to the next page |
| `reload_page` | Reload the current page |
| `navigate_to` | Navigate to a URL |
| `close_page` | Close a page |
| `scroll_screen` | Scroll the page |

### Form Filling

 | Tool | Locator |
| --- | --- |
| `fill_by_text` | Text |
| `fill_by_label` | Label |
| `fill_by_placeholder` | Placeholder |
| `fill_by_title` | Title |
| `fill_by_role` | ARIA role |

### Clicking

 | Tool | Locator |
| --- | --- |
| `click_by_text` | Text |
| `click_by_label` | Label |
| `click_by_placeholder` | Placeholder |
| `click_by_title` | Title |
| `click_by_role` | ARIA role |
| `click_by_x_y` | X/Y coordinates |

### Keyboard

 | Tool | Purpose |
| --- | --- |
| `key_press` | Send keyboard keys and shortcuts |

### Dropdowns

 | Tool | Locator |
| --- | --- |
| `select_option_by_text` | Text |
| `select_option_by_label` | Label |
| `select_option_by_placeholder` | Placeholder |
| `select_option_by_title` | Title |
| `select_option_by_role` | ARIA role |

### Checkbox & Radio Buttons

 | Tool | Locator |
| --- | --- |
| `select_checked_by_text` | Text |
| `select_checked_by_label` | Label |
| `select_checked_by_title` | Title |
| `select_checked_by_role` | ARIA role |

### Page Inspection

 | Tool | Purpose |
| --- | --- |
| `get_page_summary_tool` | Get a structured summary of the current page |

---

 ## 🔄 Example Automation Flow

 An AI agent can use the available tools to perform a sequence of browser actions.

 For example:

```
1. Open a website
        ↓
2. Receive the pageId
        ↓
3. Get the page summary
        ↓
4. Identify relevant inputs/buttons
        ↓
5. Fill required fields
        ↓
6. Click the required button
        ↓
7. Navigate or scroll if required
        ↓
8. Inspect the updated page
```

 The `pageId` returned when opening a page is used by subsequent tools to identify which browser page should be controlled.

---

 ## 📁 Project Structure

```
browser-automation-mcp/
│
├── script.py
└── README.md
```

 ### `script.py`

 Contains the MCP server implementation, browser session management, Playwright automation functions, page inspection logic, and MCP tools.

 ### `README.md`

 Project documentation and setup instructions.

---

 ## ⚙️ How It Works

 The server uses **FastMCP** to expose Python functions as MCP tools.

 The general flow is:

```
AI Agent / LLM
       │
       ▼
   MCP Client
       │
       ▼
Browser Automation MCP Server
       │
       ▼
    Playwright
       │
       ▼
   Google Chrome
       │
       ▼
     Website
```

 Each browser page receives a unique `pageId`. The server keeps track of active pages in its session so that the AI agent can specify which page each action should operate on.

---

 ## 🔎 Page Summary

 Instead of requiring an AI agent to process the entire HTML source of a webpage, the server provides a structured page summary.

 For example, the summary can identify:

```
Page
├── Metadata
├── Headings
├── Buttons
├── Links
├── Inputs
├── Checkboxes
├── Interactive Elements
├── Dialogs
├── Alerts
├── Forms
└── Text Preview
```

 This gives an AI agent useful information about the current page before deciding which browser action to perform.

---

 ## 📝 Notes

 - The browser runs in **visible mode** rather than headless mode.
- Each opened page receives a unique `pageId`.
- Multiple browser pages can be managed during a session.
- Browser interactions are performed using Playwright's asynchronous API.
- The server is designed to expose browser actions through MCP rather than providing traditional REST API endpoints.
- The MCP client must be configured with the correct path to `script.py`.

---

 ## 🤝 Contributing

 Contributions are welcome.

 If you want to improve the project:

 1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Test the browser automation tools.
5. Commit your changes.
6. Open a pull request.

---

#### Feel free to drop any suggestions and try it out yourself! ⭐ If you find this useful, consider giving the repo a star.