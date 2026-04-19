# Kanaa

A full-stack conversational AI application that enables users to ask questions and receive intelligent responses powered by Groq's LLaMA 3.1 model.

## Project Overview

Kanaa is a simple, single-interaction Q&A application where users submit one question at a time and receive an AI-generated response. Each question-response pair is stored in MongoDB Atlas for record-keeping. The application does not maintain chat history or memory between interactions—every question is treated as an independent query.

**Key Features:**
- Single question, single response interaction model
- AI-powered responses using Groq's llama-3.1-8b-instant model
- Persistent storage of all interactions in MongoDB Atlas
- Clean, minimal user interface
- Separate frontend and backend deployment

## Tech Stack

- **Backend**: Node.js + Express
- **AI Model**: Groq API (llama-3.1-8b-instant)
- **Database**: MongoDB Atlas
- **Frontend**: React + Vite
- **Deployment**: Vercel

---

*Setup instructions, deployment steps, and API documentation will be added as the project is built.*
