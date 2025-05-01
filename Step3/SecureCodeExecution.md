# Secure Code Execution in AI Agents

This document provides a detailed explanation of the code blocks in `Lesson3.ipynb`, which demonstrates secure code execution techniques for AI agents.

## Introduction

The notebook focuses on two key aspects of secure code execution:
1. Using a custom Python interpreter with restricted capabilities
2. Running code in a sandboxed environment

These security measures are essential when building AI agents that can execute code, as they help prevent potential security vulnerabilities and system abuse.

## 1. Custom Python Interpreter Setup

### Installation (Optional)
```python
#!pip install git+https://github.com/huggingface/smolagents.git
```
This commented line shows how to install the `smolagents` library directly from GitHub. It's commented out because the library is likely already installed in the environment.

### Initializing the Custom Executor
```python
from smolagents.local_python_executor import LocalPythonExecutor

custom_executor = LocalPythonExecutor(["numpy"])
```
This code imports the `LocalPythonExecutor` class from the `smolagents` library and initializes it with a list of allowed imports. In this case, only the `numpy` library is explicitly allowed, which means the executor will block attempts to import other libraries.

### Helper Function for Exception Handling
```python
def run_capture_exception(command: str):
    try:
        custom_executor(command)
    except Exception as e:
        print("ERROR:\n", e)
```
This function executes a given command using the custom executor and captures any exceptions that occur. It provides a clean way to demonstrate what happens when code attempts to perform unauthorized actions.

## 2. Security Restrictions Demonstration

### Example 1: Shell Commands
```python
# Example 1: non-defined command
# In Jupyter it works
!echo Bad command
```
This demonstrates that shell commands (prefixed with `!`) work in regular Jupyter notebooks.

```python
# In our interpreter, it does not.
harmful_command="!echo Bad command"
run_capture_exception(harmful_command)
```
When the same shell command is run through the custom executor, it fails with a syntax error. This prevents potential security risks from shell command execution.

### Allowed Imports
```python
[
    're',
    'queue',
    'random',
    'statistics',
    'unicodedata',
    'itertools',
    'math',
    'stat',
    'time',
    'datetime',
    'collections',
    'numpy'
]
```
This code block displays the list of modules that are allowed by default in the custom executor, plus the explicitly allowed `numpy` module.

### Example 2: Restricted Imports
```python
# Example 2: os not imported
harmful_command="""
import os
exit_code = os.system("echo Bad command")
"""
run_capture_exception(harmful_command)
```
This demonstrates that attempts to import unauthorized modules (in this case, `os`) are blocked by the custom executor. The `os` module is particularly sensitive as it provides access to operating system functionality.

### Example 3: Accessing Protected Modules Indirectly
```python
# Example 3: random._os.system not imported
harmful_command="""
import random
random._os.system('echo Bad command')
"""
run_capture_exception(harmful_command)
```
This shows that the custom executor also prevents attempts to access restricted modules indirectly through attributes of allowed modules. This is an important security feature as it blocks a common technique used to bypass import restrictions.

### Example 4: Infinite Loop Protection
```python
# Example 4: infinite loop
harmful_command="""
while True:
    pass
"""
run_capture_exception(harmful_command)
```
This demonstrates that the custom executor has protection against infinite loops, which could otherwise consume system resources indefinitely. The executor limits the number of iterations in loops to prevent such denial-of-service attacks.

### File System Access Risks
```python
custom_executor = LocalPythonExecutor(["PIL"])

harmful_command="""
from PIL import Image

img = Image.new('RGB', (100, 100), color='blue')

i=0
while i < 10000:
    img.save('simple_image_{i}.png')
    i += 1
"""
# custom_executor(harmful_command)
# Let's not execute this but it would not error out, and it would bloat your system with images.
```
This example (intentionally not executed) shows a potential risk with file system access. Even with restricted imports, some libraries like PIL can be used to perform potentially harmful operations like creating thousands of files that could fill up disk space.

## 3. Sandbox Execution

### Setting Up Environment Variables
```python
import os
from dotenv import load_dotenv
load_dotenv()

E2B_API_KEY = os.getenv("E2B_API_KEY")
```
This code loads environment variables from a `.env` file and retrieves the API key for E2B (Execution to Binary), a service that provides sandboxed code execution environments.

### Initializing the Sandbox Executor
The rest of the notebook (not fully shown in the excerpt) likely demonstrates how to use the E2B service to run code in a completely isolated environment, providing an additional layer of security beyond what the custom executor offers.

## Conclusion

The notebook demonstrates two complementary approaches to secure code execution:

1. **Custom Python Interpreter**: Provides a first layer of defense by restricting imports, preventing shell commands, and limiting resource usage.

2. **Sandboxed Execution**: Offers a more robust security model by running code in a completely isolated environment, preventing any access to the host system.

These security measures are essential when building AI agents that can execute code, as they help prevent potential security vulnerabilities and system abuse while still allowing the AI to perform useful computational tasks.
