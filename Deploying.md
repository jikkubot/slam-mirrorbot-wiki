# How to deploy?
Deploying is pretty much straight forward and is divided into several steps as follows:
## Installing requirements

- Clone this repo:
```
git clone https://github.com/SlamDevs/slam-mirrorbot mirrorbot/
cd mirrorbot
```

- Install requirements
For Debian based distros
```
sudo apt install python3
```
Install Docker by following the [official Docker docs](https://docs.docker.com/engine/install/debian/)

OR
```
sudo snap install docker 
```
- For Arch and it's derivatives:
```
sudo pacman -S docker python
```
- Install dependencies for running setup scripts:
```
pip3 install -r requirements-cli.txt
```

## Setting up config file
```
cp config_sample.env config.env
```
- Remove the first line saying:
```
_____REMOVE_THIS_LINE_____=True
```
Fill up rest of the fields. Meaning of each field is discussed below:
### Required Field
- `BOT_TOKEN`: The Telegram Bot Token that you got from [@BotFather](https://t.me/BotFather)
- `TELEGRAM_API`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from https://my.telegram.org. **NOTE**: DO NOT put this in quotes.
- `TELEGRAM_HASH`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from https://my.telegram.org
- `OWNER_ID`: The Telegram User ID (not username) of the Owner of the bot
- `GDRIVE_FOLDER_ID`: This is the folder ID of the Google Drive Folder to which you want to upload all the mirrors.
- `DOWNLOAD_DIR`: The path to the local folder where the downloads should be downloaded to
- `DOWNLOAD_STATUS_UPDATE_INTERVAL`: A short interval of time in seconds after which the Mirror progress/status message is updated. (I recommend to keep it to `5` seconds at least)  
- `AUTO_DELETE_MESSAGE_DURATION`: Interval of time (in seconds), after which the bot deletes it's message (and command message) which is expected to be viewed instantly. (**NOTE**: Set to `-1` to never automatically delete messages)
### Optional Field
- `ACCOUNTS_ZIP_URL`: Only if you want to load your Service Account externally from an Index Link. Archive the accounts folder to a zip file. Fill this with the direct link of that file.
- `TOKEN_PICKLE_URL`: Only if you want to load your **token.pickle** externally from an Index Link. Fill this with the direct link of that file.
- `MULTI_SEARCH_URL`: To use search/list in multiple TD/folder. Run driveid.py in your terminal and follow it. It will generate a file **drive_folder** when you finish. Upload that file [here](https://gist.github.com/) with the same file name. Open the raw file of that gist, it's URL will be your required config. Check wiki for gist related help. 
- `DATABASE_URL`: Your Database URL. See [Generate Database](https://github.com/SlamDevs/slam-mirrorbot/tree/master#generate-database) to generate database (**NOTE**: If you use database you can save your Sudo ID permanently using `/addsudo` command).
- `AUTHORIZED_CHATS`: Fill user_id and chat_id (not username) of groups/users you want to authorize. Separate them with space, Examples: `-0123456789 -1122334455 6915401739`.
- `SUDO_USERS`: Fill user_id (not username) of users whom you want to give sudo permission. Separate them with space, Examples: `0123456789 1122334455 6915401739` (**NOTE**: If you want to save Sudo ID permanently without database, you must fill your Sudo Id here).
- `IS_TEAM_DRIVE`: Set to `True` if `GDRIVE_FOLDER_ID` is from a Team Drive else `False` or Leave it empty.
- `USE_SERVICE_ACCOUNTS`: (Leave empty if unsure) Whether to use Service Accounts or not. For this to work see [Using Service Accounts](https://github.com/SlamDevs/slam-mirrorbot#generate-service-accounts-what-is-service-account) section below.
- `INDEX_URL`: Refer to https://gitlab.com/ParveenBhadooOfficial/Google-Drive-Index The URL should not have any trailing '/'
- `MEGA_API_KEY`: Mega.nz API key to mirror mega.nz links. Get it from [Mega SDK Page](https://mega.nz/sdk)
- `MEGA_EMAIL_ID`: Your E-Mail ID used to sign up on mega.nz for using premium account (Leave though)
- `MEGA_PASSWORD`: Your Password for your mega.nz account
- `BLOCK_MEGA_FOLDER`: If you want to remove mega.nz folder support, set it to `True`.
- `BLOCK_MEGA_LINKS`: If you want to remove mega.nz mirror support, set it to `True`.
- `STOP_DUPLICATE`: (Leave empty if unsure) if this field is set to `True`, bot will check file in Drive, if it is present in Drive, downloading or cloning will be stopped. (**NOTE**: File will be checked using filename, not using filehash, so this feature is not perfect yet)
- `CLONE_LIMIT`: To limit the size of Google Drive folder/file which you can clone (leave space between number and unit, Available units are (gb or GB, tb or TB), Examples: `100 gb, 100 GB, 10 tb, 10 TB`
- `MEGA_LIMIT`: To limit the size of Mega download (leave space between number and unit, available units are (gb or GB, tb or TB), Examples: `100 gb, 100 GB, 10 tb, 10 TB`
- `TORRENT_DIRECT_LIMIT`: To limit the Torrent/Direct mirror size, leave space between number and unit. Available units are (gb or GB, tb or TB), Examples: `100 gb, 100 GB, 10 tb, 10 TB`
- `TAR_UNZIP_LIMIT`: To limit the size of mirroring as Tar or unzipmirror. Available units are (gb or GB, tb or TB), Examples: `100 gb, 100 GB, 10 tb, 10 TB`
- `VIEW_LINK`: View Link button to open file Index Link in browser instead of direct download link, you can figure out if it's compatible with your Index code or not, open any video from you Index and check if its URL ends with `?a=view`, if yes make it `True` it will work (Compatible with https://gitlab.com/ParveenBhadooOfficial/Google-Drive-Index Code)
- `UPTOBOX_TOKEN`: Uptobox token to mirror uptobox links. Get it from [Uptobox Premium Account](https://uptobox.com/my_account).
- `IGNORE_PENDING_REQUESTS`: If you want the bot to ignore pending requests after it restarts, set this to `True`.
- `STATUS_LIMIT`: Limit the no. of tasks shown in status message with button. (**NOTE**: Recommended limit is `4` tasks at max).
- `IS_VPS`: (Only for VPS) Don't set this to `True` even if you are using VPS, unless facing error with web server. Also go to start.sh and replace `$PORT` by `80` or any other port you want to use.
- `SERVER_PORT`: Only For VPS even if `IS_VPS` is `False` --> Base URL Port
- `BASE_URL_OF_BOT`: (Required for Heroku to avoid sleep/idling) Valid BASE URL of app where the bot is deployed. Format of URL should be `http://myip` (where `myip` is the IP/Domain of your bot) or if you have chosen other port than `80` then fill in this format `http://myip:port`, for Heroku fill `https://yourappname.herokuapp.com` (**NOTE**: Do not put slash at the end), still got idling? You can use http://cron-job.org to ping your Heroku app.
- `RECURSIVE_SEARCH`: Set this to `True` to search in sub-folders with `/list` (**NOTE**: This will only work with shared-drive root ID. Folder IDs are not compatible with it.)
- `SHORTENER_API`: Fill your Shortener API key if you are using Shortener.
- `SHORTENER`: if you want to use Shortener in G-Drive and index link, fill Shortener URL here. Examples:
```
exe.io, gplinks.in, shrinkme.io, urlshortx.com, shortzon.com, bit.ly,
shorte.st, linkvertise.com , ouo.io
```

Above are the supported URL Shorteners. Except these only some URL Shorteners are supported.
### Add more buttons (Optional Field)
Three buttons are already added including Drive Link, Index Link, and View Link, you can add extra buttons, if you don't know what are the below entries, simply leave them, don't fill anything in them.
- `BUTTON_FOUR_NAME`:
- `BUTTON_FOUR_URL`:
- `BUTTON_FIVE_NAME`:
- `BUTTON_FIVE_URL`:
- `BUTTON_SIX_NAME`:
- `BUTTON_SIX_URL`:

## Getting Google OAuth API credential file
- Visit the [Google Cloud Console](https://console.developers.google.com/apis/credentials)
- Go to the OAuth Consent tab, fill it, and save.
- Go to the Credentials tab and click Create Credentials -> OAuth Client ID
- Choose Desktop and Create.
- Use the download button to download your credentials.
- Move that file to the root of mirrorbot, and rename it to **credentials.json**
- Visit [Google API page](https://console.developers.google.com/apis/library)
- Search for Drive and enable it if it is disabled
- Finally, run the script to generate **token.pickle** file for Google Drive:
```
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
python3 generate_drive_token.py
```

# Deploying On VPS

**IMPORTANT NOTE**: You must set `SERVER_PORT` variable to `80` or any other port you want to use.

- Start Docker daemon (skip if already running):
```
sudo dockerd
```
- Build Docker image:
```
sudo docker build . -t mirror-bot
```
- Run the image:
```
sudo docker run -p 80:80 mirror-bot
```
OR

**NOTE**: If you want to use port other than 80, change it in [docker-compose.yml](https://github.com/SlamDevs/slam-mirrorbot/blob/master/docker-compose.yml)

- Using Docker-compose, you can edit and build your image in seconds:
```
sudo apt install docker-compose
```
- Build and run Docker image:
```
sudo docker-compose up
```
- After editing files with nano for example (nano start.sh):
```
sudo docker-compose build
sudo docker-compose up
```
OR
```
sudo docker-compose up --build
```
- To stop Docker: 
```
sudo docker ps
```
```
sudo docker stop id
```
- To clear the container (this will not affect the image):
```
sudo docker container prune
```
- To delete the image:
```
sudo docker image prune -a
```
- Tutorial video from Tortoolkit repo
<p><a href="https://youtu.be/c8_TU1sPK08"> <img src="https://img.shields.io/badge/See%20Video-black?style=for-the-badge&logo=YouTube" width="160""/></a></p>

![Heroku](https://telegra.ph/file/909aa0cfc6319ce5580aa.jpg)

## Pre-requisites

- [Token Pickle](https://github.com/SlamDevs/slam-mirrorbot/wiki/Deploying#getting-google-oauth-api-credential-file)
- [Github](github.com) account
- [Heroku](heroku.com) account
	* Recommended to use 1 App in 1 Heroku account.
	* Don't use bin/fake credits card, because your Heroku account will get banned.
	* Heroku is free service, so don't expect too much.
- Text editor

## Deployment

1. Star and Fork this repo then upload **token.pickle** to your forks, or you can upload your **token.pickle** to your Index and put your **token.pickle** link to `TOKEN_PICKLE_URL` (**NOTE**: If you don't upload **token.pickle** uploading will not work).

2. Go to Repository `Settings` -> `Secrets`

	![secrets](https://telegra.ph/file/bb8cb0eced5caad68a41b.jpg)

3. Add the below Required Variables one by one by clicking `New Repository Secret` everytime.
- `HEROKU_EMAIL`: Heroku Account Email Id in which the above app will be deployed
- `HEROKU_API_KEY`: Your Heroku API key, get it from https://dashboard.heroku.com/account
- `HEROKU_APP_NAME`: Your Heroku app name, Name Must be unique
- `CONFIG_FILE_URL`: Fill [This](https://raw.githubusercontent.com/Slam-Team/slam-mirrorbot/master/config_sample.env) in any text editor. Remove the `_____REMOVE_THIS_LINE_____=True` line and fill the variables. For details about config you can see [Here](https://github.com/SlamDevs/slam-mirrorbot/wiki/Deploying#setting-up-config-file). Go to https://gist.github.com and paste your config data. Rename the file to `config.env` then create secret gist. Click on Raw, copy the link. This will be your `CONFIG_FILE_URL`. Refer to below images for clarity. 

	![steps 1 to 3](https://telegra.ph/file/1d8fec16516a87ba9d1ac.jpg)

	![step 4](https://telegra.ph/file/1491f99836cd694ea1195.jpg)

	![step 5](https://telegra.ph/file/416a550f7ded579b63272.jpg)

	* **NOTE**: Remove commit id from raw link to be able to change variables without updating the `CONFIG_FILE_URL` in secrets. should be in this form: https://gist.githubusercontent.com/username/gist-id/raw/config.env
	* Before: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/19ba5ab5eb43016422193319f28bc3c7dfb60f25/config.env
	* After: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/config.env
	* You only need to restart your bot after editing `config.env` Gist secret.

4. After adding all the above Required Variables go to Github Actions tab in your repo

5. Select `Manually Deploy to Heroku` workflow as shown below:

	![Example Manually Deploy to Heroku](https://telegra.ph/file/38ffda0165d9671f1d5dc.jpg)

6. Then click on Run workflow

	![Run workflow](https://telegra.ph/file/c5b4c2e02f585cb59fe5c.jpg)

7. **Done!** your bot will be deployed now.

## NOTE
- Don't change/edit variables from Heroku if you want to change/edit do it in `config.env` from your gist.