# Some basic Q&A:
## Got NameError: name 'cur' is not defined
- Your database issue, restart will fix it.
- Your dyno dead/App suspaneded, so your database can't connect.
## Got App Idling
- Add `BASE_URL_OF_BOT`, In README.md already explained, still got idling? You can use http://cron-job.org or http://kaffeine.herokuapp.com to ping your app
## Got FileNotFoundError: [Errno 2] No such file or directory: 'wget'
- Just refork & redeploy (delete your fork & fork again, then deploy)