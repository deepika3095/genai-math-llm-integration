# Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:
Design and implement a system where:
Users interact with a chat interface to calculate the volume of a cylinder.
User inputs such as the radius and height of the cylinder are extracted via the LLM.
The extracted inputs are passed to a Python function that calculates the volume.
The LLM integrates this function and provides the result to the user.

### DESIGN STEPS:
### STEP 1:Define the Python Function
Create a function calculate_cylinder_volume to compute the volume of a cylinder using the formula: Volume = 𝜋 × 𝑟2 × ℎ where, r is the radius and ℎ is the height.

### STEP 2: LLM Integration
Integrate the function with the LLM using a function-calling interface, allowing the LLM to invoke the Python function based on user queries.

### STEP 3: User Query Parsing
Use the LLM's ability to interpret natural language queries to extract values for radius and height.

### STEP 4: Function Invocation
Pass the extracted values to the Python function, compute the result, and return it to the LLM.

### STEP 5: Result Formatting
Present the result in a user-friendly format and provide additional guidance if necessary.
### PROGRAM:
```
NAME: DEEPIKA R
REG NO.: 212223230038
import os
import openai

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
openai.api_key = os.environ['OPENAI_API_KEY']
import json
def calculate_cylinder_volume(radius,Height):
    """Calculate the volume of a cylinder"""
    volume=3.14159*(radius**2)*height
    return json.dumps({
        "radius": radius,
        "height": height,
        "volume": volume
    })

# define a function
functions = [
    {
        "name": "calculate_cylinder_volume",
        "description": "Calculate the volume of a cylinder given radius and height",
        "parameters": {
            "type": "object",
            "properties": {
                "radius": {
                    "type": "number",
                    "description": "The radius of the cylinder in units (e.g., cm, m)",
                },
                "height": {
                    "type": "number",
                    "description": "The height of the cylinder in units (e.g., cm, m)",
                },
            },
             "required": ["radius", "height"],
        },
    }
]
messages = [
    {
        "role": "user",
        "content": "Calculate the volume of a cylinder with radius 5 and height 10."
    }
]
# Call the ChatCompletion endpoint
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions
)

print(response)
response_message = response["choices"][0]["message"]
response_message
response_message["content"]
response_message["function_call"]
json.loads(response_message["function_call"]["arguments"])
args = json.loads(response_message["function_call"]["arguments"])
calculate_cylinder_volume(**args)

```

### OUTPUT:
<img width="281" height="50" alt="image" src="https://github.com/user-attachments/assets/95e6342c-d6e5-42f7-a67a-87ac542cf3b9" />
<img width="481" height="53" alt="image" src="https://github.com/user-attachments/assets/cbfc5be0-acf9-4936-a146-e8c0088309bc" />

### RESULT:

Thus the program to design and implement a Python function for calculating the volume of a cylinder was executed successfully.
