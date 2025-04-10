# SHL Assessment Recommendation Engine

A Retrieval-Augmented Generation (RAG) system that recommends appropriate SHL assessments based on natural language queries or job descriptions.

## Project Overview

This system helps recruiters and hiring managers find suitable SHL assessments for their candidate evaluation needs. It can:
- Process natural language queries about desired assessments
- Extract job descriptions from URLs and automatically recommend assessments
- Filter assessments based on multiple criteria including job level, test type, and duration

## System Architecture

```
┌─────────────────┐    ┌───────────────────┐    ┌─────────────────────┐
│   React         │    │   FastAPI Backend │    │ Chroma Vector DB    │
│   Frontend      │────▶   with RAG        │────▶ with Google AI      │
│                 │    │   Pipeline        │    │ Embeddings          │
└─────────────────┘    └───────────────────┘    └─────────────────────┘
```

## Features

- **Natural Language Search**: Find assessments using conversational language
- **Job Description Processing**: Extract relevant skills from job postings to find assessments
- **Advanced Filtering**: Filter by job level, test type, duration, language, and more
- **API and UI**: Flexible interaction through RESTful API or user-friendly web interface

## Technical Workflow

The system operates through the following workflow:

### 1. Data Preparation Pipeline
- Assessment data is loaded from CSV files
- Data is preprocessed and cleaned
- Documents are created with structured metadata
- Vector embeddings are generated using Google's AI models
- Embeddings are stored in a Chroma vector database

### 2. Search and Recommendation Process
- **Direct Query Flow**:
  1. User enters a natural language query
  2. System extracts filters from the query (job level, test type, duration)
  3. Query is embedded and similarity search is performed against the vector database
  4. Filtered results are returned based on relevance

- **Job Description URL Flow**:
  1. User submits a URL to a job posting
  2. System extracts the job description using web scraping
  3. Google Gemini AI generates an optimized search query from the job description
  4. System performs a similarity search with the generated query
  5. Relevant assessments are returned as recommendations

### 3. Response Processing
- Results are formatted with relevant metadata
- Information includes assessment name, URL, description, duration, and test types
- Results are returned via API or displayed in the UI

## Installation and Setup

### Prerequisites
- Python 3.9+
- Node.js 18+
- Google AI API key

### Backend Setup
1. Clone the repository
   ```
   git clone https://github.com/yourusername/shl-recommendation-engine.git
   cd shl-recommendation-engine/backend
   ```

2. Install dependencies
   ```
   pip install -r requirements.txt
   ```

3. Set up environment variables
   ```
   export GOOGLE_API_KEY=your_google_api_key
   ```

4. Prepare the vector database
   ```
   python main.py --prepare assessment.csv
   ```

5. Start the API server
   ```
   python main.py --api
   ```

### Frontend Setup
1. Navigate to the frontend directory
   ```
   cd ../frontend
   ```

2. Install dependencies
   ```
   npm install
   ```

3. Configure the backend URL in `.env`
   ```
   VITE_BACKEND_DOMAIN=http://localhost:8000
   ```

4. Start the development server
   ```
   npm run dev
   ```

## Usage

### API Endpoints

- `GET /search`: Search for assessments
  - Query Parameters:
    - `query`: Text query or job URL
    - `is_url`: Boolean flag for URL processing
    - `max_results`: Maximum number of results to return

### Command Line Interface

- Prepare data: `python main.py --prepare path/to/csv`
- Process query: `python main.py --query "your query here"`
- Start API: `python main.py --api`

## Technologies Used

- **Backend**:
  - FastAPI
  - LangChain
  - Google Generative AI (Gemini)
  - Chroma Vector Database
  - BeautifulSoup for web scraping
  - Pandas for data processing

- **Frontend**:
  - React
  - TypeScript
  - Vite
  - Tailwind CSS

## Example Queries

- "I need a technical assessment for a mid-level Python developer"
- "Show me personality tests that take less than 30 minutes"
- "https://example.com/job-posting" (URL to a job description)

## Data Structure

The system uses assessment data with the following structure:
- Name: Assessment name
- URL: Link to the assessment
- Description: Detailed information
- Job levels: Target roles
- Languages: Available languages
- Test type: Assessment categories (Ability, Personality, Knowledge, etc.)
- Duration: Time in minutes
- Remote testing: Availability for remote use
- Adaptive testing: Whether the test adapts to responses

## Future Improvements

- Add user authentication
- Implement caching for improved performance
- Add support for additional languages
- Create custom assessment packages based on job requirements

## License

This project is proprietary and confidential.
