from flask import Flask, request, jsonify
import random

app = Flask(__name__)

# Sample responses for the chatbot
responses = {
    "greeting": ["Hello! How can I assist you today?", "Hi there! What travel tips do you need?"],
    "farewell": ["Goodbye! Safe travels!", "See you later! Enjoy your trip!"],
    "travel_tips": [
        "Always check the weather before you travel.",
        "Make copies of your important documents.",
        "Learn a few phrases in the local language."
    ],
    "default": ["I'm sorry, I didn't understand that. Can you ask something else?"]
}

@app.route('/chat', methods=['POST'])
def chat():
    user_input = request.json.get('message')
    response = generate_response(user_input)
    return jsonify({"response": response})

def generate_response(user_input):
    user_input = user_input.lower()
    
    if "hello" in user_input or "hi" in user_input:
        return random.choice(responses["greeting"])
    elif "bye" in user_input or "goodbye" in user_input:
        return random.choice(responses["farewell"])
    elif "tip" in user_input or "advice" in user_input:
        return random.choice(responses["travel_tips"])
    else:
        return random.choice(responses["default"])

if __name__ == '__main__':
    app.run(debug=True)
