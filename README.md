# 🛒 E-commerce AI Assistant

An LLM-powered conversational shopping assistant that can answer product and pricing queries by dynamically interacting with a product database through **function calling**.

Instead of relying entirely on the LLM's internal knowledge, the assistant can recognize when it needs external information, invoke a custom tool, retrieve the required data from a **SQLite database**, and use that result to generate the final response.

## 🚀 Project Overview

Traditional chatbots typically rely on predefined responses or the information contained within the language model itself.

This project demonstrates a more practical LLM workflow:

**User Query → LLM → Tool Selection → Database Query → Tool Response → LLM → Final Answer**

For example, when a user asks:

> "How much does the Samsung Galaxy S25 cost on Flipkart?"

the LLM can determine that it needs product information, invoke the `get_product_info` function, retrieve the relevant data from the SQLite database, and then generate a natural-language response.

The assistant is built with **Groq's GPT-OSS-120B model**, Python, SQLite and Gradio.

## ✨ Key Features

* 💬 **Natural-language product queries**
* 🧠 **LLM-powered decision making**
* 🔧 **Function/tool calling**
* 🗄️ **SQLite database integration**
* 🔄 **Iterative tool execution and response generation**
* 🧾 **Conversation history support**
* 🖥️ **Interactive Gradio chat interface**
* 🚫 **Reduced hallucination by retrieving product information from a database**

## 🏗️ How It Works

The application follows a tool-calling workflow:

### 1. User sends a query

The user interacts with the assistant through the Gradio chat interface.

### 2. LLM processes the query

The user's message, conversation history and system instructions are sent to the LLM.

The model has access to a custom function:

`get_product_info(product_name)`

### 3. LLM decides whether a tool is required

If the question requires product information, the model generates a **tool call** rather than attempting to answer from its own knowledge.

### 4. Tool queries the database

The application extracts the product name from the model-generated tool call and executes a query against the SQLite product database.

### 5. Tool result is returned to the LLM

The database result is passed back to the model as a tool response.

### 6. LLM generates the final response

The model uses the retrieved information along with the conversation context to produce the final natural-language answer.

This process can be repeated whenever the model generates another tool call.

## 🧠 Architecture

```text
                 ┌─────────────────┐
                 │      User       │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │    Gradio UI    │
                 └────────┬────────┘
                          │
                          ▼
              ┌───────────────────────┐
              │      LLM (Groq)       │
              │     GPT-OSS-120B      │
              └───────────┬───────────┘
                          │
                 Needs product data?
                    /            \
                  No              Yes
                  │                │
                  │                ▼
                  │       ┌─────────────────┐
                  │       │ Function Call   │
                  │       │get_product_info │
                  │       └────────┬────────┘
                  │                │
                  │                ▼
                  │       ┌─────────────────┐
                  │       │ SQLite Database │
                  │       └────────┬────────┘
                  │                │
                  │                ▼
                  │       ┌─────────────────┐
                  │       │  Tool Response  │
                  │       └────────┬────────┘
                  │                │
                  └────────┬───────┘
                           ▼
                 ┌─────────────────┐
                 │  Final Response │
                 └─────────────────┘
```

## 🛠️ Tech Stack

| Technology        | Purpose                         |
| ----------------- | ------------------------------- |
| **Python**        | Core application logic          |
| **Groq**          | LLM inference                   |
| **GPT-OSS-120B**  | Language model                  |
| **SQLite**        | Product data storage            |
| **Gradio**        | Conversational user interface   |
| **python-dotenv** | Environment variable management |

## 📦 Project Structure

```text
E-commerce-AI-Assistant/
│
├── ecommerce_AI_assistant.ipynb   # Main project notebook
├── products.db                    # SQLite product database
└── README.md                      # Project documentation
```

## ⚙️ Setup

### 1. Clone the repository

```bash
git clone https://github.com/Oorja-Gund28/E-commerce-AI-Assistant.git
cd E-commerce-AI-Assistant
```

### 2. Install dependencies

```bash
pip install groq gradio python-dotenv openai
```

### 3. Add your Groq API key

Create a `.env` file in the project directory:

```env
GROQ_API_KEY=your_api_key_here
```

### 4. Run the notebook

Open:

```text
ecommerce_AI_assistant.ipynb
```

Run the cells sequentially and launch the Gradio interface.

## 💡 Example Queries

Try asking:

```text
How much is the Macbook?
```

```text
What is the price of the Samsung Galaxy S25?
```

```text
Which platform has the iPhone 17?
```

```text
Tell me about the Dell XPS 15.
```

The assistant retrieves product information through its database tool before generating the response.

## 🎯 What This Project Demonstrates

This project was built to explore how LLM applications can move beyond simple prompt-and-response interactions.

The key concepts demonstrated are:

* **LLM function calling**
* **Tool integration**
* **LLM-to-database interaction**
* **Structured tool definitions**
* **Tool result handling**
* **Conversational context**
* **Iterative LLM workflows**
* **Building interactive LLM applications with Gradio**


## 👩‍💻 Author

**Oorja Gund**

Data Analyst | Data Science & AI | GenAI & LLM Applications
