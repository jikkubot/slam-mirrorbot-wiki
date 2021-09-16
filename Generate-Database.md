## 1. Using ElephantSQL
- Go to https://elephantsql.com and create account (skip this if you already have **ElephantSQL** account)
- Hit **Create New Instance**
- Follow the further instructions in the screen
- Hit **Select Region**
- Hit **Review**
- Hit **Create instance**
- Select your database name
- Copy your database url, and fill to `DATABASE_URL` in config

## 2. Using Heroku PostgreSQL
- Log into [Heroku](https://id.heroku.com/login)
- Create a new Heroku app
	* Once you see your personal app dashboard, you can create a new app. If your dashboard is currently empty, you can click the **Create new app** button. Otherwise click the **New** button in the top-right corner and select **Create new app**
	* Since you only need the app to get access to your database, the **App name** doesn't really matter and you can choose whatever you want. In the screenshot below, `get-my-db` is used as an **App name**
- Add a PostreSQL database
	* To attach a PostgreSQL database to the app you just created, you need to navigate to the **Resources** tab in the header of your newly created app's dahsboard. Then type **Heroku Postgres** into the **Add-ons** search field.

When shown, select the suggested **Heroku Postgres**
	* The next popup asks you to choose a pricing plan for the database. Select the **Hobby Dev - Free plan** and click **Provision**
- Congratulations, you now created a free PostgreSQL database