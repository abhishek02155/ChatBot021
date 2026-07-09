# ChatBot by python
CodeAlpha- Task 2 
This is a simple rule-based chatbot built as part of the CodeAlpha Python Programming Internship (Task 4).
The chatbot responds to common user inputs such as greetings, questions about itself, and farewells, using a set of predefined rules.
Features
Responds to greetings (e.g., "hello", "hi", "hey")
Replies to questions like "how are you"
Answers questions about its name and capabilities
Responds to "thank you" messages
Ends the conversation when the user types "bye", "goodbye", "exit", or "quit"
Provides a default response for unrecognized input
Concepts Used
if-elif conditional statements
Functions
Loops (while)
Input/output handling
String manipulation (lowercasing and stripping input)

import wikipedia
import requests

def get_response(user_input):
    text = user_input.lower().strip()

    # Greetings
    if "hello" in text or "hi" in text:
        return "Hi! How can I help you today?"

    # Wikipedia queries
    elif "who is" in text or "tell me about" in text:
        try:
            return wikipedia.summary(user_input, sentences=2)
        except:
            return "Sorry, I couldn't find an answer."

    # Weather queries
    elif "weather" in text:
        city = text.split("weather in")[-1].strip()
        api_key = "YOUR_OPENWEATHER_API_KEY"
        url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
        data = requests.get(url).json()
        if data.get("main"):
            temp = data["main"]["temp"]
            return f"The current temperature in {city} is {temp}°C."
        else:
            return "Sorry, I couldn't fetch the weather."

    # Default fallback
    else:
        return "I'm still learning. Try asking me about a person, weather, or news!"

