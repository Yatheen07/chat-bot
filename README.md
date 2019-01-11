# chat-bot
A full tutorial on how to create a simple chatbot using python and dialogflow.

## Steps to be followed in dialogflow console.

### Step 0: 
- Create an free account on `google cloud platform` (allows two projects).
- Create an account in `dialogflow console`.

### Step 1: Creating an agent
- In the left navigation bar, Select `Pre-built agent` to create a new agent.
- Select `Jokes` from the available choices and click import
- Select the `settings`, and modify the agent name and click create.

### Step 2: Create an Entity
- In the left navigation bar, click `Entity` --> `Create` Entity.
- Create an entity named bot and declare the synonyms as `bot,you,yourself,your`,etc.
- Allow `automated exapnsion`
- click save

### Step 3: Create an intent 
- In the left navigation bar, click `Intents` --> `Create` Intent.
- Give the Intent name as `info.basic` and click `save`.
- Specify around 4 to 5 training phrases to train the bot.
- Give a text response and add variations! 
- Click save!

### Step 4: Test your bot in the right side panel

### Step 5: Downloading your service account key
- Navigate to settings of your joker-bot.
- Click Project-id ( You will be taken into your GCP console)
- Click the navigation menu and click API and services --> Credentials
- Click Create Credentials and select Service-account
- Select a new service account from dropdown menu and give a service account name
- Select ROLE --> Dialogflow --> Dialogflow API Client
- Click Create. [JSON file will be downloaded]

## Steps to be followed in python

### Step 0: Install dialogflow using pip

> python -m pip install dialogflow

### Step 1: Import the os package and link the service-key you just downlaoded.

```python
import os
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = r"YOUR_CREDENTIAL_PATH"
```

### Step 2: Operations with dialogflow

```python
import dialogflow_v2 as df
```
create a client object for that session and use that obect to create session path.

```python
session_client = df.SessionClient()
session = session_client.session_path("YOUR_PROJECT_ID","SESSION_NUMBER")
```

Project_id is available in your `dialogflow console`.
Session_id is a random number.

### Step 3: Creating a very simple console chat interface

```python
while True:
  print("=" * 40)
  inputText = input("User: ")
  if(inputText == "stop" or inputText =="break"):
    break
  text_input = df.types.TextInput(text = text2,language_code = "en") 
  query_input = df.types.QueryInput(text = text_input)
  response = session_client.detect_intent(session=session, query_input=query_input)
  try:
        response_text = response.query_result.fulfillment_messages[0].simple_responses.simple_responses[0].text_to_speech
    except:
        response_text = "Am not sure about that!"
  print('Response: {} \n'.format(response_text))      
 ``` 
 
Thats it!
