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
git reset --hard
git pull
```
#### Having problems with time on local machine, fx can't update files to S3
```
sudo ntpdate manager.ournodes.com
```

#### Authorization header cannot be found in Laravel, but through apache getallheaders()
```
    public\.htaccess in the <IfModule mod_rewrite.c>
    
    # Pass Authorization header with request
    # (known php-cgi bug)
    RewriteCond %{HTTP:Authorization} ^(.+)$
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
```

### Middleware not loaded during tests

If you have custom middleware on a project, and you are running tests, you will face something like: 

`Class 'riide.api' not found`

There is an issue with Dingo that's causing this, and the quick workaround is simple:

- Go to config/app.php
- Find the service providers
- Load the `Nodes\Api\ServiceProvider::class` **JUST BEFORE** the `App\Providers\RouteServiceProvider::class`

This will solve the issue.

### DS store files
# remove any existing files from the repo, skipping over ones not in repo
find . -name .DS_Store -print0 | xargs -0 git rm --ignore-unmatch
# specify a global exclusion list
git config --global core.excludesfile ~/.gitignore
# adding .DS_Store to that list
echo .DS_Store >> ~/.gitignore

or add globally to gitignore

```git config --global core.excludesfile /Users/mat/.gitignore```