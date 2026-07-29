# 🤖 End-to-End Agentic Chatbot

An autonomous, stateful **Agentic AI Chatbot** built with **LangGraph**, **Streamlit**, and **Python**. This system moves beyond simple prompt-response interactions by integrating dynamic tool usage, long-term state persistence, Human-in-the-Loop (HITL) execution guardrails, and automated multi-cloud deployment pipelines.

---

## 🌟 Key Features

* **LangGraph Agentic Workflow:** Graph-based orchestration managing state, multi-step tool calls, and conditional routing.
* **Human-in-the-Loop (HITL) Control:** Pause-and-resume checkpointers allow human verification before critical execution steps.
* **External Tool Integration:** Equipped with real-time web search (Tavily) and live data retrieval APIs (OpenWeather).
* **State & Memory Persistence:** Stateful conversation tracking with dynamic thread handling and message history reducers.
* **Observability:** Integrated with **LangSmith** for full execution tracing, token tracking, and debugging.
* **Production-Ready Docker Build:** Optimized, containerized, non-root user image equipped with CORS/WebSocket production flags.
* **Automated CI/CD:** GitHub Actions workflows for automated builds, Docker Hub pushes, and AWS EC2 updates.

---

## 🛠️ System Architecture

```plaintext
  User Input (Streamlit UI)
            │
            ▼
   ┌─────────────────┐
   │ LangGraph State │ ◄── Checkpoint / Persistence (RAM/DB)
   └────────┬────────┘
            │
      [Chat Node]
            │
   ┌────────┴────────┐
   │ Needs Tool Call? │
   └────┬───────┬────┘
    Yes │       │ No
        ▼       ▼
  [Tool Node]  [Human Approval / Interrupt State (HITL)]
  - Tavily       │
  - Weather      ▼
        └──────► Output Response to Streamlit UI
```



## 🚀 Quickstart Guide (Local Development)

1. Clone the Repository
```
	git clone [https://github.com/Mrinmoy2002-prog/End-to-End-Agentic-Chatbot.git](https://github.com/Mrinmoy2002-prog/End-to-End-Agentic-Chatbot.git)
	cd End-to-End-Agentic-Chatbot
```

2. Set Up Virtual Environment & Install Dependencies
```
	python -m venv venv
	source venv/bin/activate  # On Windows use: venv\Scripts\activate
	pip install -r requirements.txt
```

3. Environment Configuration
```
	Create a .env file in the root directory and add your API keys:

		Code snippet
		# LLM & Tools
		MISTRAL_API_KEY=your_mistral_api_key
		TAVILY_API_KEY=your_tavily_api_key
		OPENWEATHER_API_KEY=your_openweather_api_key

		# LangSmith Observability
		LANGSMITH_TRACING=true
		LANGSMITH_ENDPOINT="[https://api.smith.langchain.com](https://api.smith.langchain.com)"
		LANGSMITH_API_KEY=your_langsmith_api_key
		LANGSMITH_PROJECT="agentic-chatbot"
```

4. Run Locally
```
	streamlit run app.py
```
### 🐳 Running with DockerBuild
```
	ImageBashdocker build -t agentic-chatbot .
	Run ContainerBashdocker run -d \
	-p 8501:8501 \
	--env-file .env \
	--name agentic-app \
	agentic-chatbot
```
Access the application at http://localhost:8501.☁️ Deployment Pipelines1. 

### Streamlit Cloud (Recommended for Quick Hosting)
```
	Fork or push this repository to GitHub.
	Sign in to Streamlit Community Cloud.
	Connect your repository, set the main file to app.py.
	Add your secrets under Advanced Settings $\rightarrow$ Secrets and click Deploy.
	```
2. AWS EC2 with GitHub Actions (Automated CI/CD)
```
	The project includes a .github/workflows/deploy.yml pipeline that:
	Triggers on every git push to main.
	Builds and pushes the Docker container to Docker Hub.
	SSHs into an AWS EC2 instance, prunes old containers/images, and runs the updated container over port 8501.3. Hugging Face Spaces (Docker SDK)
	Create a new Space on Hugging Face using the Docker SDK.
	Add environment variables under Settings $\rightarrow$ Variables and secrets.
	Push the code repository to Hugging Face Git remote.
```

## 📂 Project StructurePlaintext├── .github/
```│   └── workflows/
│       └── deploy.yml          # GitHub Actions CI/CD pipeline
├── .streamlit/
│   └── config.toml             # Production WebSocket & CORS configurations
├── app.py                      # Main Streamlit user interface
├── agent.py                    # LangGraph workflow, nodes, and checkpointers
├── tools.py                    # External API tools (Tavily, Weather, etc.)
├── requirements.txt            # Python dependencies
├── Dockerfile                  # Container definition
├── .env.example                # Example environment variable layout
└── README.md                   # Project documentation
```

📜 LicenseThis project is licensed under the MIT License.