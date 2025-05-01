# Code Agent

A comprehensive project for exploring AI code agents and their capabilities, featuring step-by-step lessons on building and deploying intelligent agents.

## Description

This repository contains a series of Jupyter notebooks that demonstrate how to build, monitor, and deploy AI code agents. Each step builds upon the previous one, gradually introducing more complex concepts and capabilities.

## Project Structure

The project is organized into multiple steps, each focusing on different aspects of AI code agents:

- **Step2**: Building a simple code agent with basic tools
- **Step4**: Monitoring and evaluating agent performance
- **Step5**: Building a deep research-like agent with web search capabilities

## Step-by-Step Guide

### Step 2: Building a Simple Code Agent

The `Step2` directory contains a notebook (`Lesson2.ipynb`) that demonstrates how to build a simple code agent with the following components:

- **Environment Setup**: Importing libraries and setting up authentication
- **Data Preparation**: Creating sample datasets for ice cream suppliers
- **Tool Creation**: Defining specialized tools for calculations
- **Model Setup**: Initializing a language model using Hugging Face API
- **Agent Configuration**: Creating and configuring a `CodeAgent`
- **Agent Execution**: Running the agent with specific queries
- **Complex Problem Solving**: Handling multi-factor analyses

### Step 4: Monitoring and Evaluating Your Agent

The `Step4` directory contains a notebook (`Lesson4.ipynb`) that focuses on:

- **Setting up tracing**: Configuring OpenTelemetry for monitoring agent behavior
- **Tracing agent runs**: Capturing detailed information about agent execution
- **Building evaluation systems**: Creating metrics to assess agent performance
- **Analyzing tool usage**: Understanding when and how agents use different tools

### Step 5: Building a Deep Research Agent

The `Step5` directory contains a notebook (`Lesson5.ipynb`) that demonstrates:

- **Web search integration**: Using Tavily API to search the web
- **Multi-agent systems**: Creating specialized agents for different tasks
- **Data visualization**: Generating maps and charts based on research findings
- **Quality control**: Validating agent outputs against requirements

## Getting Started

### Prerequisites

- Python 3.13 (recommended, but 3.11+ should work)
- Virtual environment tool (venv, conda, etc.)
- Jupyter Notebook or JupyterLab

### Environment Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Rupeebw/coding-agent.git
   cd coding-agent
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### API Keys Setup

Create a `.env` file in the root directory with the following API keys:

```
HF_API_KEY=your_huggingface_api_key
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
DLAI_LOCAL_URL=http://localhost:{port}/
```

### Running the Notebooks

1. Start Jupyter:
   ```bash
   jupyter notebook
   ```

2. Navigate to the desired step directory (e.g., `Step2`, `Step4`, or `Step5`)
3. Open the corresponding notebook (e.g., `Lesson2.ipynb`, `Lesson4.ipynb`, or `Lesson5.ipynb`)
4. Run the cells sequentially

## Dependencies and Troubleshooting

### Critical Dependencies

- **smolagents==1.13.0**: Core library for building code agents
- **openai==1.66.3**: Required for OpenAI models
- **tavily-python==0.5.1**: Required for web search functionality
- **nbformat>=4.2.0**: Required for notebook processing
- **plotly==6.0.1**: Required for data visualization
- **pandas==2.2.3** and **numpy==2.2.3**: Required for data manipulation

### Common Issues and Solutions

1. **OpenTelemetry Connection Errors**:
   - If you encounter connection errors with OpenTelemetry in Step4, modify the code to use a console exporter instead of Phoenix.
   - Alternatively, ensure a collector is running on the specified port.

2. **API Key Issues**:
   - Ensure all required API keys are correctly set in your `.env` file
   - Check that the `.env` file is in the root directory
   - Verify that `load_dotenv()` is called before accessing environment variables

3. **Model Selection**:
   - The notebooks use different models (Hugging Face models, OpenAI models)
   - If you prefer using OpenAI models, ensure you have the correct API key and modify the model initialization code

4. **Memory Issues**:
   - Some models require significant memory
   - If you encounter memory errors, try using a smaller model or reducing batch sizes

5. **Visualization Issues**:
   - If maps don't display correctly in Step5, ensure plotly and its dependencies are correctly installed
   - Try running `pip install plotly --upgrade` if needed

## Model Preferences

The default configuration uses:
- OpenAIServerModel with gpt-4.1-mini for code generation
- This can be changed to other models based on your preference and API access

## License

This project is licensed under the MIT License - see the LICENSE file for details.
