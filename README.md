# ✈️ n8n AI Travel Agent & Supporting Travel MCP Server

A modular, privacy-focused travel recommendation assistant built in **n8n** using **LangChain Agent architecture**. The agent utilizes local LLMs via **Ollama (`qwen3:8b`)**, retains user preference session history, and connects dynamically via **Model Context Protocol (MCP)** to a specialized **Travel MCP Server** for live data retrieval.

---

## 🏗️ Architecture Overview

The project is split into two interconnected n8n workflows:

```text
[ Client Request ] ──(POST)──► [ Webhook ] ──► [ Set Input ]
                                                    │
                                                    ▼
                                           [ AI Agent Node ] ◄──► [ Memory Buffer Window ]
                                           (Ollama qwen3:8b)
                                                    │
                                           (MCP Protocol via SSE)
                                                    │
                                                    ▼
                                        [ Travel MCP Server ]
                                        ├── geocode_city   (Geoapify)
                                        ├── search_places  (Geoapify)
                                        └── get_weather    (wttr.in)
