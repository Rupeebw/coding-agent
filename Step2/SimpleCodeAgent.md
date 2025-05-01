# Code Agent

A project for exploring AI code agents and their capabilities.

## Description

This repository contains code and notebooks for working with AI code agents, including examples and experiments with various AI models and techniques.

## Building a Simple Code Agent (Step2)

The `Step2` directory contains a notebook (`Lesson2.ipynb`) that demonstrates how to build a simple code agent. Here's a breakdown of the key components:

### 1. Environment Setup
- Importing necessary libraries (pandas, numpy, PIL, etc.)
- Setting up warning controls and environment variables
- Loading authentication tokens for API access

### 2. Data Preparation
- Creating a sample dataset of ice cream suppliers with details like:
  - Supplier name and location
  - Distance in kilometers
  - Whether the supplier is Canadian (affects tariffs)
  - Price per liter and tasting fees

### 3. Tool Creation
- Defining specialized tools using the `@tool` decorator from the `smolagents` library:
  - `calculate_transport_cost`: Calculates transportation costs based on distance and order volume
  - `calculate_tariff`: Calculates import tariffs for Canadian products

### 4. Model Setup
- Initializing a language model using the Hugging Face API
- Using the Qwen2.5-72B-Instruct model with specific parameters:
  - Maximum token length: 4096
  - Temperature: 0.1 (for more deterministic responses)

### 5. Agent Configuration
- Creating a `CodeAgent` with:
  - The initialized language model
  - The custom tools created earlier
  - Maximum steps for execution (10)
  - Authorized Python imports (pandas, numpy)
  - Verbosity level for debugging

### 6. Agent Execution
- Running the agent with specific queries
- The agent processes the query, determines which tools to use, and executes the appropriate code
- Results are returned in a structured format

### 7. Complex Problem Solving
- Demonstrating how the agent can handle more complex requests
- Creating comparative analyses of supplier costs considering multiple factors

## Getting Started

### Dependencies

* Python 3.9+
* Required packages are listed in requirements.txt

### Installing

```
pip install -r requirements.txt
```

### Usage

Run the Jupyter notebooks to explore different examples and experiments:

1. Navigate to the `Step2` directory
2. Open `Lesson2.ipynb` in Jupyter Notebook or Jupyter Lab
3. Run the cells to see the code agent in action

## License

This project is licensed under the MIT License - see the LICENSE file for details.
