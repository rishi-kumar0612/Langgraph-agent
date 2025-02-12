# Finance Agent Project 🚀

## Description
This project is a financial assistant that answers questions about stocks, companies, and financial data. It uses multiple specialized agents to fetch raw data from financial APIs, perform web research, and finally summarize the results for the user. The system is built using **LangGraph**, which organizes these agents into a clear, step-by-step workflow.

---

## Project Structure 🗂️

1. **main.py**  
   - Contains the entry point for the application.  
   - Starts the app in interactive mode (asking the user for questions) or processes a single query passed via the command line.  
   - Builds the application using a workflow defined in another file and handles user queries asynchronously.

2. **graph.py**  
   - Builds a state graph that controls the workflow of the assistant.  
   - Defines four key agents:
     - **Supervisor Agent** – Decides which specialized agent should work next based on the conversation and user query.
     - **Financial Data Agent** – Retrieves raw financial information (e.g., stock prices, company profiles, ratios) using API tools.
     - **Web Research Agent** – Gathers additional information from web pages when needed.
     - **Output Summarizing Agent** – Compiles and summarizes the data from the other agents to form the final answer.
   - Connects these agents in a series of steps, starting with the supervisor and ending with the final summary.

3. **tools.py**  
   - Contains functions (or “tools”) that directly call external APIs (such as the Financial Modeling Prep API) to get data like stock prices, financial ratios, and company profiles.  
   - Also includes a tool to read and extract text from webpages for web research.

---

## How It Works ⚙️

- **Workflow Setup:**  
  The application builds a workflow (or state graph) where each node represents one of the agents. This graph defines the order in which agents operate. For example, after the Supervisor Agent selects the Financial Data Agent, the data is retrieved and sent back to the supervisor, which then decides if another agent is needed or if it’s time to summarize the answer.

- **Processing a Query:**  
  When a user submits a question (via interactive mode or the command line), the question is wrapped as a message and sent through the workflow:
  - The **Supervisor Agent** analyzes the conversation and decides which specialized agent should process the next part of the task.
  - The **Financial Data Agent** uses various tools to fetch raw financial data (e.g., stock prices, profiles, ratios).
  - If more context is needed, the **Web Research Agent** visits webpages and extracts relevant information.
  - Finally, the **Output Summarizing Agent** compiles all gathered information into a clear, concise summary as the final answer.

- **Asynchronous Processing:**  
  The project uses Python’s asynchronous programming (async/await) to efficiently handle queries and API calls without waiting for each task to complete sequentially.

---

## Why LangGraph Over LangChain 🤔

Imagine you have a team where each person is an expert in a specific task—one checks the facts, another looks up extra details on the internet, and a third writes a summary. **LangGraph** acts like a clear roadmap that tells each team member when to do their part. This step-by-step process ensures that all tasks are handled in order, resulting in a more organized and accurate answer.

While **LangChain** is like a toolbox for language tasks, **LangGraph** provides the overall plan that connects everything together. Its graph-based approach offers better clarity on the sequence of operations and dependencies between agents, making it easier to add or modify nodes without disrupting the entire workflow.

---

## Future Improvements and Further Features 🌟

- **More Data Sources:**  
  Integrate additional financial data APIs to improve the accuracy and variety of information.

- **Enhanced Decision Making:**  
  Improve the Supervisor Agent’s ability to select the best agent based on a deeper understanding of the query.

- **Advanced Analytics:**  
  Add features for financial trend analysis, risk assessment, and predictive analytics.

- **Better User Interface:**  
  Develop a web-based or mobile interface to simplify user interactions.

- **Improved Error Handling:**  
  Enhance logging and error reporting to quickly identify and fix issues during data retrieval or processing.

- **Customization Options:**  
  Allow users to tailor responses based on their specific interests or investment strategies.

---

## Use Cases 💼

- **Investors:**  
  Quickly retrieve summaries of company performance, stock prices, and key financial metrics.

- **Financial Analysts:**  
  Access raw financial data to perform further analysis or build financial models.

- **Casual Users:**  
  Get easy-to-understand summaries of financial information and news.

- **Researchers:**  
  Combine financial data with additional web-sourced information for comprehensive reports.

---

## Summary 📝

This project demonstrates a structured way to build a multi-agent financial assistant. By using **LangGraph** to manage the flow of tasks, the system efficiently gathers, processes, and summarizes complex financial data. It’s like having a team of experts where each one knows exactly when to step in, ensuring you receive an organized and accurate answer every time.
