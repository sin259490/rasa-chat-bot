# rasa-chat-

# A simple Rasa chatbot example
# This project demonstrates how to set up a basic Rasa chatbot using Docker and Docker Compose.example
# Requirements:
# - Docker
# - Docker Compose  
# - Rasa 3.6.2
# - Python 3.8 or higherexample
# Usage:
# 1. Clone the repository:
#    git clone


# start the Rasa server:  detached mode:
docker-compose up -d

# top the current services:
docker-compose down

# train the model
docker run -v $(pwd):/app rasa/rasa:3.6.2 train --domain domain.yml --data data --out models

# Now that the model is trained, let's start the Rasa server:
docker-compose up


# Test greeting
curl -X POST http://localhost:5005/webhooks/rest/webhook \
  -H "Content-Type: application/json" \
  -d '{"sender": "test", "message": "Hello"}'

# Test Claude Sonnet query
curl -X POST http://localhost:5005/webhooks/rest/webhook \
  -H "Content-Type: application/json" \
  -d '{"sender": "test", "message": "Is Claude Sonnet enabled?"}'

# Test mood
curl -X POST http://localhost:5005/webhooks/rest/webhook \
  -H "Content-Type: application/json" \
  -d '{"sender": "test", "message": "I am feeling great"}'