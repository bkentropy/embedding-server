# Embedding Service

A FastAPI-based service for generating text embeddings using Sentence Transformers.

## Features

- Generate embeddings for text or lists of text
- Health check endpoint
- Containerized with Docker

## API Endpoints

- `POST /embed` - Generate embeddings for the provided text(s)
  - Request body: `{"texts": ["text1", "text2", ...]}`
  - Response: `{"embeddings": [[...], [...], ...]}`

- `GET /health` - Health check endpoint
  - Response: `{"status": "healthy"}`

### Hitting an endpoint
```
curl -X POST localhost:8111/embed -d @example.json -H "Content-Type: application/json"
curl -X POST localhost:8111/embed --json @example.json
```

## Running with Docker

1. Build the Docker image:
   ```bash
   docker build -t embedding-service .
   ```

2. Run the container:
   ```bash
   docker run -d -p 8111:8111 --name embedding-service embedding-service
   ```

### Or with docker-compose
```
docker compose up -d
```

## Local Development

1. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the service:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8111 --reload
   ```

The service will be available at `http://localhost:8111`

## Nomad Deployment

1. Build the Docker image:
   ```bash
   docker build -t embedding-service .
   ```

2. Deploy with Nomad:
   ```bash
   nomad run embedding.nomad.hcl
   ```

3. Check job status:
   ```bash
   nomad status embedding-service
   ```

4. View logs:
   ```bash
   nomad logs -job embedding-service
   ```

5. Stop the service:
   ```bash
   nomad stop embedding-service
   ```

The service will be available through Nomad's service discovery at the configured port 8111.
# Embedding Models

## The all-MiniLM-L6-v2
