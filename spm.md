# SPM (STL Package Manager)
## Setup
In admin dashboard, there is a page that allows admin to fetch the source code of specific bot.  
Once the code is fetched, the admin has to fill in a form, and the form will be converted into `config.py`.
There is one example of `config.py`  
Original:
```
SERVER_IP = 1
TOKEN = 2
ADMIN_EMAIL = 3
```
Then the `config.py` will be converted into a form that asks admin to fill in the three fields. After the form is submitted, a new `config.py` will be generated.  
Converted:
```
SERVER_IP = "1.2.3.4"
TOKEN = "ct8b4yf89-3k4xy89f"
ADMIN_EMAIL = "admin@example.com"
```
So the application can use this configuration file to setup the bot.
Finally, the admin can press the `install` button and install the bot.

## Running
After pressing `install`, the main backend application will open a thread for a bot.  
Therefore, if the main application is down, the bot will be down together.  
When the bot is running, admin can see it on the admin dashboard page.
