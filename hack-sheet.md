#### Restart apache - if you cant access your local sites
```
sudo service apache2 restart
```

#### Set git repo to github repo from composer package (Backend in this example)
```
cd vendor/nodes/backend/
git init
git remote add origin git@github.com:nodes-php/backend.git
git add -A
git reset —hard
git pull
```
#### Having problems with time on local machine, fx can't update files to S3
```
sudo ntpdate manager.ournodes.com
```

