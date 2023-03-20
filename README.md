# ChatBot with Telebot and OpenAI

This is just simple chatbot for Telegram with OpenAI library.

# Deployment process

1. Create `main.py` file with ChatBot
2. Save your ML model in a pickle format
3. After that we need to record all packages were installed for our bot, so we can later install it on server, to do it, execute next command: `pip freeze > requirements.txt`. If you have problems with `pip freeze` try `pipreqs` library.
4. Creating Dockefile. Example in this repository.
5. Creating Fly.io account (connect it with your GitHub). You will be asked for payment details. But giving them to Fly.io is not necessary, just press “Try Fly.io for free” under form for card details, and proceed to next page of Get Started landing pages. But if you see an error connecting with you payment details you can add payment details. Don't afraid about payment process - you can delete you card info after running server.
6. To interact with Fly.io platform we need a special CLI utility called flyctl.
windows: `iwr https://fly.io/install.ps1 -useb | iex`
linux/mac: `curl -L https://fly.io/install.sh | sh`
7. So, after command execution you shall be able to use flyctl from your Terminal (Command line), to check if it installed successfully type `flyctl --help` on Windows CMD. Under Linux, to be able to use flyctl, you can be asked to add flyctl bin folder to PATH, so last lines of script output for instructions if command not recognized. If `flyctl --help` gave you an output for available commands, then installation process was successful.
8. To authorize your flyctl in fly.io use next command: `flyctl auth login`
9. Now we need to create our app on Fly.io. In folder with main.py execute next command `flyctl apps create <your-app-name>`
10. Set secret with our Telegram bot token. To provide our Telegram Bot a secret token, we can provide it to fly.io directly, so it will be automatically put into environment of our container with bot. To do that execute next command: `flyctl secrets set TELEGRAM_TOKEN=<your telegram bot token>`
11. Create fly.io configuration file - `fly.toml`. Example in this repository.
12. After all this actions you shall be able to deploy your application with next command: `flyctl deploy`

This command will automatically build and deploy your docker container with telegram bot, and after that it will launch it in cloud.
So after all that stuff, as we didn’t encountered any error, we probably want to check how everything working. So let’s go to telegram and send /start command to our bot. And also, in fly.io dashboard, we can check monitoring tab for our application and check there is logging of our messages going in logs.
