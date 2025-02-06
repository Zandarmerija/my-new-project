# my-new-project
Building AI course project
# AI-Powered Mental Health Chatbot

Final project for the Building AI course

## Summary
An AI-powered chatbot designed to provide mental health support by offering immediate, empathetic responses and guiding users to appropriate resources. The chatbot uses natural language processing to understand user emotions and provide tailored advice.

## Features
- **Empathetic Responses**: The chatbot provides supportive and understanding responses.
- **Sentiment Analysis**: Detects the user's emotional state to tailor responses.
- **Resource Suggestions**: Offers links to mental health resources and hotlines.
- **Simple Interface**: Easy-to-use command-line interface.

## How to Use
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/mental-health-chatbot.git
   pip install -r requirements.txt
python chatbot.py

---

### 2. `requirements.txt`

```plaintext
transformers==4.26.0
torch==1.13.0
nltk==3.7
import torch
from transformers import pipeline, AutoModelForCausalLM, AutoTokenizer
from nltk.sentiment import SentimentIntensityAnalyzer
import nltk
import random

# Download NLTK data for sentiment analysis
nltk.download('vader_lexicon')

# Load a pre-trained conversational model (e.g., DialoGPT)
model_name = "microsoft/DialoGPT-medium"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Initialize a chatbot pipeline
chatbot = pipeline("text-generation", model=model, tokenizer=tokenizer)

# Initialize sentiment analyzer
sia = SentimentIntensityAnalyzer()

# Load mental health resources
def load_resources():
    with open("resources/mental_health_resources.txt", "r") as file:
        return file.readlines()

resources = load_resources()

# Define a function to simulate a mental health chatbot
def mental_health_chatbot():
    print("Welcome to the Mental Health Chatbot. Type 'exit' to end the conversation.")
    chat_history = []

    while True:
        user_input = input("You: ")
        if user_input.lower() == "exit":
            print("Chatbot: Take care of yourself. Remember, you're not alone. Goodbye!")
            break

        # Analyze sentiment of the user input
        sentiment = sia.polarity_scores(user_input)
        if sentiment['compound'] < -0.5:
            print("Chatbot: I'm really sorry to hear that you're feeling this way. Let's talk more about it.")
        elif sentiment['compound'] > 0.5:
            print("Chatbot: I'm glad to hear that you're feeling positive! How can I assist you further?")
        else:
            print("Chatbot: I'm here to listen. How can I help you today?")

        # Generate a response using the chatbot model
        response = chatbot(user_input, max_length=50, pad_token_id=tokenizer.eos_token_id)
        bot_response = response[0]['generated_text']

        # Add some empathetic phrases to make the chatbot more supportive
        supportive_phrases = [
            "I'm here for you.",
            "That sounds tough. How can I help?",
            "You're not alone in this.",
            "It's okay to feel this way.",
            "Let's talk more about it."
        ]
        bot_response = bot_response + " " + random.choice(supportive_phrases)

        print(f"Chatbot: {bot_response}")

        # Suggest a resource if the sentiment is negative
        if sentiment['compound'] < -0.5:
            print(f"Chatbot: Here's a resource that might help: {random.choice(resources)}")

        chat_history.append((user_input, bot_response))

# Run the chatbot
if __name__ == "__main__":
    mental_health_chatbot()
National Suicide Prevention Lifeline: 1-800-273-TALK (8255)
Crisis Text Line: Text HOME to 741741
BetterHelp Online Therapy: https://www.betterhelp.com
7 Cups of Tea: https://www.7cups.com
Mindfulness and Meditation Resources: https://www.headspace.com
git clone https://github.com/your-username/mental-health-chatbot.git
pip install -r requirements.txt
python chatbot.py
Welcome to the Mental Health Chatbot. Type 'exit' to end the conversation.
You: I've been feeling really stressed lately.
Chatbot: I'm really sorry to hear that you're feeling this way. Let's talk more about it.
Chatbot: I'm here for you. It sounds like you're going through a tough time. How can I help?
Chatbot: Here's a resource that might help: National Suicide Prevention Lifeline: 1-800-273-TALK (8255)
You: I don't know what to do.
Chatbot: That sounds tough. How can I help? Sometimes talking about it can help. Let's talk more about it.
You: exit
Chatbot: Take care of yourself. Remember, you're not alone. Goodbye!
