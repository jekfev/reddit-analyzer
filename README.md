# Reddit Content Miner & Auto-Publisher (n8n Workflow)

Automated n8n workflow for mining top community discussions, processing topics with AI, and scheduling content generation.

## 🛠 What it does

1. **Scheduled Reddit Ingestion:** Periodically fetches top posts from targeted niche subreddits (e.g., plant care and gardening communities).
2. **Smart Filtering & Deduplication:**
* Filters out non-problem posts and low-engagement threads.
* Performs dual-layer deduplication (programmatic Jaccard similarity + semantic LLM analysis using Google Gemini) to avoid repetitive content.


3. **AI Content Generation:** Translates raw community pain points into structured, human-like editorial topics and generates conversational posts.
4. **Automated Publishing:** Manages a content queue via internal data tables and publishes scheduled posts to a messenger channel (e.g., MAX platform).

## ⚙️ Architecture & Tech Stack

* **Orchestration:** [n8n](https://n8n.io/) (Low-code workflow automation)
* **AI / LLM:** Google Gemini API (Flash for processing/deduplication, Pro for content creation)
* **Data Layer:** n8n Data Tables
* **APIs:** Reddit REST API (OAuth2 / HTTP Request nodes)

## 🚀 Workflow Structure

* **Branch A (Topic Mining):** Runs daily at 07:00. Fetches posts -> Filters problems -> Runs strict & semantic deduplication -> Stores clean topics in the database.
* **Branch B (Publishing Pipeline):** Runs daily at 10:00. Retrieves the highest-scoring new topic -> Generates a native-style post via LLM -> Publishes to the target channel -> Updates status to `published`.
