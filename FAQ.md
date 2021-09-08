# Some basic Q&A:

### How/Help?
- Before asking please read/check [README.md](https://github.com/SlamDevs/slam-mirrorbot/blob/master/README.md).

### Got error 403/404
- You can read https://developers.google.com/drive/api/v3/handle-errors, this link about all error code from Google Drive.

### Got NameError: name 'cur' is not defined
- Your database issue, restart will fix it.
- Your dyno dead/App suspaneded, so your database can't connect.

### Got App Idling issue
- Add `BASE_URL_OF_BOT`, In readme already explained, still got idling? You can use http://cron-job.org or http://kaffeine.herokuapp.com to ping your app

### I have issue with Service Accounts
- You forgot to upload accounts folder or you forgot to redeploy, check this by sending /shell ls, if accounts folder is there, then this is not the problem
- The service accs' names are not renamed to 0.json, 1.json, ... Check this by sending `/shell ls accounts`, if the names are randomized, get the sarename script, run it outside accounts folder, and upload accounts folder again, and redeploy
- Service accs are not in your team drive you choose in gdrive folder id, check it by going to your team drive. Check if the service accs are there (within or without in google groups, both will work)
- Gdrive folder id invalid

### How to add custom filenames for the files?
- https://telegra.ph/Magneto-Python-Aria---Custom-Filename-Examples-01-20