# Alexa Skill Examples

## Links
### Adminstration
* [Amazon Developer Console](https://developer.amazon.com)
* [Amazon Alexa](https://alexa.amazon.com)
* [Amazon Alexa (de)](https://alexa.amazon.de)
* [History of your voice interactions with Alexa (Settings - History)](https://alexa.amazon.de/spa/index.html?#settings/dialogs)
* [Voice Training](https://www.amazon.com/gp/help/customer/display.html?nodeId=201601940)

### Fun
* [List of known easter eggs for Amazon Echo (so far)](https://www.reddit.com/r/amazonecho/comments/2v15fx/list_of_known_easter_eggs_for_amazon_echo_so_far)

> "Alexa, what's the answer to life, the universe, and everything?"

> "Alexa, what are the laws of robotics?" compare her answer with <a href="https://en.wikipedia.org/wiki/Laws_of_robotics">Laws of robotics<a>

### Technical
* [Understanding How Users Interact with Skills](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/understanding-how-users-interact-with-skills)
* [Choosing the Invocation Name for a Custom Skill](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/choosing-the-invocation-name-for-an-alexa-skill)
* [Slot Type Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference)

### Tutorial
* [Alexa Python Tutorial](https://developer.amazon.com/de/alexa-skills-kit/alexa-skill-quick-start-tutorial)
* [Build an Alexa Skill with Python and AWS Lambda](http://moduscreate.com/build-an-alexa-skill-with-python-and-aws-lambda)
* [Developing Alexa Skills (Training by Big Nerd Ranch)](https://developer.amazon.com/de/alexa-skills-kit/big-nerd-ranch)

### Flask Ask
* [Flask-Ask: A New Python Framework for Rapid Alexa Skills Kit Development](https://developer.amazon.com/de/blogs/post/tx14r0iyygh3skt/flask-ask:-a-new-python-framework-for-rapid-alexa-skills-kit-development)
* [Flask-Ask Documentation](https://flask-ask.readthedocs.io/en/latest)
* [Deploy Flask-Ask Skills to AWS Lambda with Zappa](https://developer.amazon.com/blogs/alexa/post/8e8ad73a-99e9-4c0f-a7b3-60f92287b0bf/new-alexa-tutorial-deploy-flask-ask-skills-to-aws-lambda-with-zappa)

#### Known Issues
Before installing Flask-Ask you need to downgrade pip:
```
# pip install pip==9.0.3
```
After installing Flask-Ask with all its dependencies you need to downgrade the cryptography module:
```
# pip install 'cryptography<2.2'
```

### ngrok
* [ngrok - Secure tunnels to localhost](https://ngrok.com)

## Examples
### Setup the Skill Service
> The examples are intended to run on your workstation.
* Install python 2.7.x with pip
* Install flask-ask
```
# pip install flask-ask
... or ...
# pip2 install flask-ask
```
* Open a secure tunnel to localhost with ngrok
```
# ./ngrok http 5000

ngrok by @inconshreveable                                                                                                                                                                                                                                             (Ctrl+C to quit)

Session Status                online
Update                        update available (version 2.2.8, Ctrl-U to update)
Version                       2.2.4
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://d1c7b569.ngrok.io -> localhost:5000
Forwarding                    https://d1c7b569.ngrok.io -> localhost:5000

Connections                   ttl     opn     rt1     rt5     p50     p90
                              17      0       0.00    0.00    0.45    0.65

HTTP Requests
-------------

POST /                         200 OK
```
* You'll need the HTTPS endpoint (here https://d1c7b569.ngrok.io) for your skill configuration. You need to update the HTTPS endpoint each time you start ngrok.

### Configure the Skill
#### Skill Information Settings
* Leave the "Skill Type" set to "Custom Interaction Model"
* Enter "Account Balance" (without quotes) for both the "Name" and "Invocation Name" fields.

#### Interaction Model Settings
* Copy the JSON in alexa-skill-examples/all_account_intents.json into the "Intent Schema" field.
* Configure utterances (if you like to) in the "Sample Utterances" field.

#### Configuration Settings
* Make sure the HTTPS radio button is selected for the "Endpoint" field.
* Enter the HTTPS endpoint from ngrok into the textfield.
* Don't bother with "Account Linking".

#### SSL Certificate Settings
> It's important to choose the second radio button with the following label because that's what ngrok uses.
```
My development endpoint is a subdomain of a domain that has a wildcard certificate from a certificate authority.
```

### Basic Interaction
<img src="https://rawgithub.com/marcsauter/alexa-skill-examples/master/images/interaction.svg">

### Account Balance
```
# cd account_balance
# python account_balance.py
```

All Account Balances are hard-coded. There would be a request to your Account Service.

### Account Balance with pin
```
# cd account_balance_pin
# python account_balance_pin.py
```

Your PIN is **1984**. The PIN is hard-coded.

### Account Balance with Security Question
```
# cd account_balance_pet
# python account_balance_pet.py
```

Your favorite pet is a **monkey**. The Answer is hard-coded.

# Presentation

To start the presentation install [[https://golang.org/dl/][The Go Programming Language]] for your Operating System.
```
go get golang.org/x/tools/cmd/present
cd <path to alexa-skill-examples>/presentations/alexa
present -notes -base ../www -http=<hostname>:<port>
```


