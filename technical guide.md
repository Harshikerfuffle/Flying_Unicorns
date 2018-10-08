**Technical Guide**: How to use dialogueflow to extract intents from user inputs, map it to our code and give users output<br />
**by**: Harshika Jain, MIIPS Adv 2018 <br />
**Course**: 49714-A1
___
**What is DialogFlow?** <br />
Previously known as API.AI, this became known as DialogFlow after being acquired by Google. It offers NLP for building into a chatbot interface such as keyword matching, understanding human speech to derive intent and meaning etc.<br />

The way it can be used:

![Alt text](https://g.gravizo.com/source/custom_mark13?https%3A%2F%2Fraw.githubusercontent.com%2FTLmaK0%2Fgravizo%2Fmaster%2FREADME.md)
<details> 
<summary></summary>
custom_mark13
@startuml;
actor User;
participant "First Class" as A;
participant "Second Class" as B;
participant "Last Class" as C;
User -> A: DoWork;
activate A;
A -> B: Create Request;
activate B;
B -> C: DoWork;
activate C;
C -> B: WorkDone;
destroy C;
B -> A: Request Created;
deactivate B;
A -> User: Done;
deactivate A;
@enduml
custom_mark13
</details>

![Alt text](https://g.gravizo.com/source/custom_mark13?https%3A%2F%2Fraw.githubusercontent.com%2FTLmaK0%2Fgravizo%2Fmaster%2FREADME.md)
<details> 
<summary></summary>
custom_mark13
@startuml;
User->Text/ Messenger: Types something
Text/ Messenger->Ruby: Sent via Twilio
Ruby->Dialogflow: intent detection on dialogflow
Dialogflow->Ruby: conveys intent
Ruby->Text/ Messenger:intent mapped to specified response
Text/ Messenger->User:user sees response on his phone
@enduml
custom_mark13
</details>

