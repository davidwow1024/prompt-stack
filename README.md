# prompt-stack

Compose interactive terminal prompts using stackable, modular components. Designed for building complex CLI input flows with ease.

<div align="center">

![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![PyPI](https://img.shields.io/pypi/v/prompt-stack.svg)
![Status](https://img.shields.io/badge/status-stable-brightgreen.svg)

</div>

> 🚅 **Interactive prompts made simple.** Build a prompt like stacking blocks.

## ✨ Features

*   **Stackable Architecture:** Chain components together using a fluent, intuitive API.
*   **Modular Components:** Mix and match input types (text, choice, confirm, password, file).
*   **Rich Styling:** Full support for ANSI colors, emojis, and custom visual themes.
*   **Dynamic Validation:** Apply type checking and custom validators at every stack level.
*   **Flow Control:** Manage conditional logic between prompt steps seamlessly.
*   **Cross-Platform:** Works reliably on Linux, macOS, and Windows terminals.
*   **Extensible:** Create your own custom prompt blocks to fit specific needs.
*   **Minimal Dependencies:** Lightweight implementation for fast CLI startup.

## 📦 Installation

Install `prompt-stack` via pip:

```bash
pip install prompt-stack
```

## 🛠 Usage

The core concept is building a prompt flow by stacking components. Each block represents a step in the interaction.

### 1. Simple Input Flow
Create a basic authentication flow by stacking a text input and a confirmation step.

```python
from prompt_stack import Stack

def main():
    result = (
        Stack()
        .text("username", "Enter your username: ")
        .text("password", "Enter password: ", mask="*")
        .confirm("proceed", "Proceed with login?")
        .run()
    )

    if result.proceed:
        print(f"Logging in as {result.username}...")

if __name__ == "__main__":
    main()
```

### 2. Complex Selection & Validation
Handle multi-step configuration with validation and multiple choice options.

```python
from prompt_stack import Stack, Select, Choice

def setup_server():
    config = (
        Stack()
        .select("region", "Select deployment region:", ["us-east", "eu-west", "ap-south"])
        .choice("features", "Enable features:", ["logging", "monitoring", "backup"], multiple=True)
        .text("port", "Server Port:", validator=lambda x: 1024 <= int(x) <= 65535)
        .run()
    )
    
    return config
```

### 3. Custom Styling
Apply a custom theme to your stack for a unique terminal look.

```python
from prompt_stack import Stack, Theme

# Define a custom theme
neon_theme = Theme(
    prompt_color="cyan",
    input_color="white",
    success_color="green",
    error_color="red"
)

# Apply theme to stack
Stack().set_theme(neon_theme).text("name", "Who are you?").run()
```

## ⚙️ Configuration

`prompt-stack` can be configured via environment variables or a local `prompt-stack.yaml` file.

**Environment Variables:**
*   `PROMPT_STACK_THEME`: Set default theme (e.g., `dark`, `light`, `custom`).
*   `PROMPT_STACK_TIMEOUT`: Set input timeout in seconds.

**Configuration File:**
Create a `prompt-stack.yaml` in your project root:

```yaml
theme:
  prompt_color: "#00ff00"
  error_prefix: "[!]"
defaults:
  timeout: 30
  retry_count: 3
```

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.