# Kanaa

A full-stack conversational AI application that enables users to ask questions and receive intelligent responses powered by Groq's LLaMA 3.1 model.

🔗 **Live Demo**: [https://kanaa-xt3x.vercel.app](https://kanaa-xt3x.vercel.app)

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

### Why This Stack?

**Node.js + Express**: Industry-standard backend combination with excellent stability, extensive documentation, and seamless Vercel deployment support. Express provides a lightweight, unopinionated framework perfect for building RESTful APIs.

**Groq API (llama-3.1-8b-instant)**: Offers fast inference times with a generous free tier (6,000 requests/day, 500,000 tokens/minute). The 8B parameter model provides quality responses while maintaining low latency—ideal for real-time Q&A interactions.

**MongoDB Atlas**: Cloud-hosted NoSQL database that requires no server management. Its flexible document structure is perfect for storing question-response pairs, and the free tier is sufficient for development and moderate production use.

**React + Vite**: Vite provides lightning-fast development experience with hot module replacement. React's component-based architecture makes it easy to build and maintain the UI. Together, they offer modern development practices with minimal configuration.

**Vercel**: Zero-config deployment platform with excellent support for both Node.js backends and React frontends. Built-in environment variable management, automatic HTTPS, and global CDN make it ideal for this project.

## Setup Instructions

### Prerequisites

- Node.js (v18 or higher)
- npm or yarn
- MongoDB Atlas account ([sign up here](https://www.mongodb.com/cloud/atlas/register))
- Groq API key ([get one here](https://console.groq.com))
- Git

### Backend Setup

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/kanaa.git
cd kanaa/backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**

Create a `.env` file in the `backend` directory:
```env
GROQ_API_KEY=your_groq_api_key_here
MONGODB_URI=your_mongodb_atlas_connection_string_here
PORT=5000
```

**Getting your MongoDB URI:**
- Log in to MongoDB Atlas
- Click "Connect" on your cluster
- Choose "Connect your application"
- Copy the connection string and replace `<password>` with your database password

4. **Start the development server**
```bash
npm run dev
```

The backend will run on `http://localhost:5000`

### Frontend Setup

1. **Navigate to frontend directory**
```bash
cd ../frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**

Create a `.env` file in the `frontend` directory:
```env
VITE_BACKEND_URL=http://localhost:5000
```

4. **Start the development server**
```bash
npm run dev
```

The frontend will run on `http://localhost:5173`

### Running the Full Application Locally

1. Open two terminal windows
2. In terminal 1: Start the backend (`cd backend && npm run dev`)
3. In terminal 2: Start the frontend (`cd frontend && npm run dev`)
4. Open your browser to `http://localhost:5173`

## Deployment Steps

### Prerequisites for Deployment

- GitHub account
- Vercel account ([sign up here](https://vercel.com/signup))
- Push your code to a GitHub repository

### Backend Deployment on Vercel

1. **Log in to Vercel** and click "Add New Project"

2. **Import your GitHub repository**

3. **Configure the project**
   - **Root Directory**: Set to `backend`
   - **Framework Preset**: Other
   - **Build Command**: Leave empty
   - **Output Directory**: Leave empty
   - **Install Command**: `npm install`

4. **Add environment variables**
   
   Go to "Environment Variables" and add:
   - `GROQ_API_KEY` = your Groq API key
   - `MONGODB_URI` = your MongoDB Atlas connection string
   - `PORT` = 5000

5. **Deploy**

   Click "Deploy" and wait for the deployment to complete.

### Frontend Deployment on Vercel

1. **Add a new project** in Vercel (separate from backend)

2. **Import the same GitHub repository**

3. **Configure the project**
   - **Root Directory**: Set to `frontend`
   - **Framework Preset**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`

4. **Add environment variables**
   
   Go to "Environment Variables" and add:
   - `VITE_BACKEND_URL` = your deployed backend URL (e.g., `https://kanaa-liard.vercel.app`)

5. **Deploy**

   Click "Deploy" and your frontend will be live

### Deployed URLs

- **Frontend**: [https://kanaa-xt3x.vercel.app](https://kanaa-xt3x.vercel.app)
- **Backend**: [https://kanaa-liard.vercel.app](https://kanaa-liard.vercel.app)

## API Documentation

### Base URL

**Local Development**: `http://localhost:5000`  
**Production**: `https://kanaa-liard.vercel.app`

### Endpoints

#### POST /api/ask

Submits a question to the AI model and returns the generated response.

**Request:**

```http
POST /api/ask
Content-Type: application/json

{
  "question": "What is the capital of France?"
}
```

**Request Body Parameters:**

| Parameter | Type   | Required | Description                    |
|-----------|--------|----------|--------------------------------|
| question  | string | Yes      | The user's question to the AI |

**Response (Success - 200 OK):**

```json
{
  "answer": "The capital of France is Paris."
}
```

**Response Body Fields:**

| Field  | Type   | Description                        |
|--------|--------|------------------------------------|
| answer | string | The AI-generated response          |

**Error Responses:**

**400 Bad Request** - Missing or invalid question
```json
{
  "error": "Question is required"
}
```

**500 Internal Server Error** - Server or API error
```json
{
  "error": "Failed to process request"
}
```

### Example Usage

**Using cURL:**
```bash
curl -X POST https://kanaa-liard.vercel.app/api/ask \
  -H "Content-Type: application/json" \
  -d '{"question": "What is the capital of France?"}'
```

**Using JavaScript (Fetch API):**
```javascript
const response = await fetch('https://kanaa-liard.vercel.app/api/ask', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    question: 'What is the capital of France?'
  }),
});

const data = await response.json();
console.log(data.answer);
```

## Database Schema

Each interaction is stored in MongoDB with the following structure:

```javascript
{
  _id: ObjectId,
  question: String,      // User's question
  response: String,      // AI-generated answer
  timestamp: Date        // When the interaction occurred
}
```

## Project Structure

```
kanaa/
├── backend/
│   ├── node_modules/
│   ├── .env
│   ├── .gitignore
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── node_modules/
│   ├── public/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── App.css
│   │   ├── main.jsx
│   │   └── index.css
│   ├── .env
│   ├── .gitignore
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── .gitignore
├── README.md
└── vibecoded.md
```

## Security Best Practices

- All API keys and database credentials are stored in environment variables
- `.env` files are excluded from version control via `.gitignore`
- CORS is properly configured to allow necessary origins
- No sensitive information is hardcoded in the source code

## License

MIT
