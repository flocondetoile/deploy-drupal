# drupal-deploy
automatic drupal deploy with gitlab

You can select the branch for auto pull, this is util for Development and Production Server config.

---

##On your server

install Drush

You need to generate and config SSH Key for apache user
in virtualhost add

```bash
RewriteEngine on
RewriteRule .* - [E=X-GITLAB-TOKEN:%{HTTP:X-Gitlab-Token}]
```

### Gitlab 

http://doc.gitlab.com/ce/ssh/README.html

When you have done ssh config, you can do "git pull" without put your password

In your drupal folder (public_html or something) you need put the drupal-deploy folder with __deploy.php__ and __config.sample.php__

rename config.sample.php in config.php

Change your configuration in config.php  File.

```PHP
define('TOKEN', 'MYTOKEN'); // This TOKEN put in Payload URL in GitLab
define('REMOTE_REPOSITORY', 'git@gitlab.com:MYWEBSITE.git');
define('DIR','/var/www/MYWEBSITE/'); // It's important that the path ends with '/'
define('BRANCH','refs/heads/master'); // (Gitlab branch Route)
define('LOGFILE', "log.txt"); // Log File Name
define('GIT', '/usr/bin/git'); // Unix git command route
define('DRUSH', '/usr/bin/drush'); // Unix git command route
```

---

## On GitLab

In your project:

Settings -> Web Hooks  

Url: http://yoursite.com/drupal-deploy/deploy.php

Secret Token: MYTOKEN

Select Just the push event. 

Add WebHook
