# Archiving the Repo 

Moving this to [Clientx Implementation Samples](https://github.com/clientx-platform/implementation-examples).

-----



# Clientx Agent Bot Demo using Rasa

> You should be running this demo on a local installation of Clientx and a non dockerised setup for the `localhost` and `ports` to be accessible for all the services involved. If you are intending to run in a remote server, ensure you change the localhost urls with appropriate IP addresses and make sure the ports should be accessible for all the services involded. 

This is a sample implementation of agent bot capabilities in clientx using [rasa](https://rasa.com/) . Rasa Open Source is a machine learning framework to automate text- and voice-based assistants.

You can refer the [rasa documentation](https://rasa.com/docs/rasa/user-guide/installation/) to get it up and running in your machine. 








## Get a rasa project up and running. 

Go to a new directory and create a rasa project. If you have rasa installed in your machine you can get it up and running by follow in commands.  Refer [docs](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/) to get the installation up and running. 

```
mkdir rasa
cd rasa
rasa init --no-prompt
```

go to `credentials.yml` file in the directory and ensure the following value is set. This is to ensure we can communicate with rasa through rest api

```
rest:
  # you don't need to provide anything here - this channel doesn't
  # require any credentials
```

start the rasa server with following command

```
 rasa run -m models --enable-api --log-file out.log
```

##  Get your clientx up and create an agent bot

go to your clientx directory and ensure your local server is running.  Start a rails console in your directory.

```
bundle exec rails c
```

Inside the rails console, type the following commands to create an agent bot and get its access token. Save the retrieved token as you would need it in further step.

```
bot = AgentBot.create!(name: "Rasa Bot", outgoing_url: "http://localhost:8000")
bot.access_token.token
```

Connect Agent Bot to your inbox by running the following command

```
AgentBotInbox.create!(inbox: Inbox.first, agent_bot: bot)
```


```
## Using Python
open up the python file in your editor and change the follow values with appropriate ones. 

rasa_url, clientx_url and clientx_bot_token.

Then run `pip install -r requirements.txt` and `python3 -m gunicorn --workers=1 test:app -b 0.0.0.0 `

## Using PHP:
open up the `rasa-router/index.php` file in your editor and change the follow values with appropriate ones. 

```
$rasa_url = 'http://localhost:5005';
$clientx_url = 'http://localhost:3000';
$clientx_bot_token = '<your agent bot token>';
```

run the php server  in the rasa-router directory

```
cd rasa-router
php -S localhost:8000
```

