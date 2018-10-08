**Technical Guide**: How to use dialogueflow to extract intents from user inputs, map it to our code and give users output<br />
**by**: Harshika Jain, MIIPS Adv 2018 <br />
**Course**: 49714-A1
___
**What is DialogFlow?** <br />
Previously known as API.AI, this became known as DialogFlow after being acquired by Google. It offers NLP for building into a chatbot interface such as keyword matching, understanding human speech to derive intent and meaning etc.<br />

The way it can be used:
![alt text](https://github.com/Harshikerfuffle/flying-unicorns/blob/master/dialogflow_ruby1.png)

### Implementation<br />
**1. In DialogFlow**<br />
For setting up Dialogflow, an account needs to be set up and an agent needs to be created. Here are the tutorials for the same:<br />
- Create a dialogflow account: (https://dialogflow.com/docs/getting-started/create-account)<br />
- Create an agent: (https://dialogflow.com/docs/getting-started/first-agent)<br />
- Where to find your project_id (will be used later in .env file)<br />

![alt text](https://github.com/Harshikerfuffle/flying-unicorns/blob/master/image3.png)

**Adding intents in Dialogflow**

- A helpful video: (https://www.youtube.com/watch?v=2CVP6xe2ssk)<br />
- How to make an intent screenshot<br />
Example intent name: EventIntent<br />
Training phrases: “upcoming events”, “events”, “upcoming birthdays”<br />

![alt text](https://github.com/Harshikerfuffle/flying-unicorns/blob/master/image1.png)

**2. In Text Editor**
- Also refer to the following code repo which has examples of adding dialogflow to ruby: <br /> https://github.com/GoogleCloudPlatform/ruby-docs-samples/blob/master/dialogflow/detect_intent_texts.rb

```
Require "securerandom"
 def detect_intet_texts project_id:, session_id:, texts:, language_code:
  # [START dialogflow_detect_intent_text]
  # project_id = "Your Google Cloud project ID"
  # session_id = "mysession"
  # texts = "hello", "book a meeting room"]
  # language_code = "en-US"

  require "google/cloud/dialogflow"
  session_client = Google::Cloud::Dialogflow::Sessions.new
  session = session_client.class.session_path project_id, session_id
  puts "Session path: #{session}"

 texts.each do |text|
    query_input = { text: { text: text, language_code: language_code } }
    response = session_client.detect_intent session, query_input
    query_result = response.query_result

    puts "Query text:        #{query_result.query_text}"
    puts "Intent detected:   #{query_result.intent.display_name}"
    puts "Intent confidence: #{query_result.intent_detection_confidence}"
    puts "Fulfillment text:  #{query_result.fulfillment_text}\n"
    
    return query_result.intent.display_name
  end
  
  # [END dialogflow_detect_intent_text]
End

def determine_response (body)
    body = body.downcase.strip
    no = "i didnt quite understand what you mean"
    
    project_id = ENV["GOOGLE_CLOUD_PROJECT"]
    intent = detect_intent_texts project_id: project_id,
                            session_id: SecureRandom.uuid,
                            texts: [body],
                            language_code:"en-US"
        
    if intent == "EventIntent"
      response = "no upcoming events"
    end
    
    return response
```
<br />
**3. In Gemfile**
```
gem 'google-cloud-dialogflow', '~> 0.2.2'
```
<br />
**4. In .env file**
```
GOOGLE_CLOUD_PROJECT = "your_project_id"
GOOGLE_APPLICATION_CREDENTIALS = $PWD/service_account.json
```
The api can do the rest of the work of finding your unique project id in the text editor.<br />

**5. In Terminal**
```gem install google-cloud-dialogflow```
How to set up google cloud api in the Heroku environment variables:
- Works after cd and the file path
- This is done to ensure that intents from dialogflow can be received by heroku, sent to our code and the intent be mapped to the output


