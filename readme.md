Below is a detailed report on how the Finance Agent project works, along with explanations on why LangGraph was chosen over LangChain. The report is written in simple, plain text—as you might include in a GitHub README file.

─────────────────────────────  
Finance Agent Project  
─────────────────────────────

Description:  
This project is a financial assistant that answers questions about stocks, companies, and financial data. It uses multiple specialized agents to fetch raw data from financial APIs, perform web research, and finally summarize the results for the user. The system is built using LangGraph, which helps organize these agents into a clear, step-by-step workflow.

─────────────────────────────  
Project Structure:  

1. **main.py**  
   - This file contains the entry point for the application.  
   - It starts the app in interactive mode (asking the user for questions) or processes a single query passed via the command line.  
   - The main function builds the application using a workflow defined in another file and then handles the user’s query asynchronously.

2. **graph.py**  
   - This file builds a state graph that controls the workflow of the assistant.  
   - It defines four key agents:  
     a. **Supervisor Agent** – Decides which specialized agent should work next based on the conversation and user query.  
     b. **Financial Data Agent** – Retrieves raw financial information (like stock prices, company profiles, and ratios) using API tools.  
     c. **Web Research Agent** – Gathers additional information from web pages when needed.  
     d. **Output Summarizing Agent** – Compiles and summarizes the data from the other agents to form the final answer.  
   - The workflow connects these agents in a series of steps, starting with the supervisor and ending with the final summary.

3. **tools.py**  
   - This file contains functions (or “tools”) that directly call external APIs (such as the Financial Modeling Prep API) to get data like stock prices, financial ratios, and company profiles.  
   - It also includes a tool to read and extract text from webpages for web research.

─────────────────────────────  
How It Works:  

- **Workflow Setup:**  
  The application builds a workflow (or state graph) where each node represents one of the agents. This graph defines the order in which agents operate. For example, after the supervisor agent selects a financial data agent, the data is retrieved and then sent back to the supervisor. The supervisor then decides if another agent is needed or if it’s time to summarize the answer.

- **Processing a Query:**  
  When a user submits a question (either via interactive mode or command line), the question is wrapped as a message and sent through the workflow.  
  - The **Supervisor Agent** analyzes the conversation and decides which specialized agent should process the next part of the task.  
  - The **Financial Data Agent** uses various tools to fetch raw financial data (stock prices, profiles, ratios, etc.).  
  - If more context is needed, the **Web Research Agent** can visit webpages and extract relevant information.  
  - Finally, the **Output Summarizing Agent** takes all the gathered information and produces a clear, concise summary as the final answer.

- **Asynchronous Processing:**  
  The project uses Python’s asynchronous programming (async/await) so that it can process queries and API calls efficiently without waiting for each task to complete sequentially.

─────────────────────────────  
Why LangGraph Over LangChain – Technical Explanation:  

LangGraph provides a graph-based approach to building workflows. In this project, it helps structure the entire conversation into a state graph where each node is a specialized agent. This design offers better clarity on the sequence of operations and dependencies between agents. With LangGraph, you can easily see and manage the flow from data fetching to web research and finally to output summarization. Although LangChain is powerful for LLM-based applications, LangGraph simplifies complex, multi-step processes by allowing developers to add or modify nodes without disturbing the overall workflow.

─────────────────────────────  
Why LangGraph Over LangChain – Non-Technical Explanation:  

Imagine you have a team where each person is an expert in a specific task—one checks the facts, another looks up extra details on the internet, and a third writes a summary. LangGraph acts like a clear roadmap that tells each team member when to do their part. This step-by-step process makes sure that all tasks are handled in order, resulting in a more organized and accurate answer for your question. LangChain is like a toolbox that helps with language tasks, but LangGraph gives you the overall plan that connects everything together.

─────────────────────────────  
Future Improvements and Further Features:  

- **More Data Sources:**  
  Integrate additional financial data APIs to improve the accuracy and variety of information.

- **Enhanced Decision Making:**  
  Improve the supervisor agent’s ability to select the best agent based on a deeper understanding of the query.

- **Advanced Analytics:**  
  Add features for financial trend analysis, risk assessment, and predictive analytics.

- **Better User Interface:**  
  Develop a web-based or mobile interface to make interacting with the assistant easier.

- **Improved Error Handling:**  
  Enhance logging and error reporting to quickly identify and fix issues during data retrieval or processing.

- **Customization Options:**  
  Allow users to tailor responses based on their specific interests or investment strategies.

─────────────────────────────  
Use Cases:  

- **Investors:**  
  Quickly retrieve summaries of company performance, stock prices, and key financial metrics.

- **Financial Analysts:**  
  Access raw financial data to perform further analysis or build financial models.

- **Casual Users:**  
  Get easy-to-understand summaries of financial information and news.

- **Researchers:**  
  Combine financial data with additional web-sourced information for comprehensive reports.

─────────────────────────────  
This project demonstrates a structured way to build a multi-agent financial assistant. By using LangGraph to manage the flow of tasks, the system can efficiently gather, process, and summarize complex financial data.