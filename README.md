import openai
import os

openai.api_key = "sk-proj-UCf7Gh3Pq9Xa2ZLm4Rt6Yw8Nv0Bd5Kj1HrQeCsTuVoMiXpAzEnLbYcDgFkSjWhUoPlRaA"
openai.api_base = os.getenv("OPENAI_API_BASE")

message = ""
messages = []
system_msg = input("What type of chatbot would you like to create?\n")
messages.append({"role": "system", "content": system_msg})

print("\nYour new assistant is ready!")
print("Start by typing a message and pressing enter. To quit, type STOP\n")

while message != "STOP":
    message = input("You: ")
    if message == "STOP":
        break
    else:
        messages.append({"role": "user", "content": message})
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=messages
        )

        reply = response.choices[0].message["content"]
        messages.append({"role": "assistant", "content": reply})
        print("\nBOT: " + reply + "\n")
print("Chatbot Session Ended")
