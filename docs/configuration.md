---
id: configuration
title: Project Configuration
sidebar_label: Project Configuration
---

## Apply Patches

Copy the patch files from 'temp' folder of the project to virtualenv Django

```shell
$ cd CollaborationSystem
```
### Django-Reversion Compare
```shell
$ cp temp/patch_for_reversion_compare.py collab/lib/python3.5/site-packages/reversion_compare/views.py
```

### Machina (Discussion Forum)
```shell
$ cp temp/board_base.html collab/lib/python3.5/site-packages/machina/templates/machina/board_base.html
```
### Django-Notifications
```shell
$ cp temp/notifications/models.py collab/lib/python3.5/site-packages/notifications/models.py
$ cp temp/notifications/urls.py collab/lib/python3.5/site-packages/notifications/urls.py
$ cp temp/notifications/views.py collab/lib/python3.5/site-packages/notifications/views.py
$ cp temp/notifications/notifications_tags.py collab/lib/python3.5/site-packages/notifications/templatetags/notifications_tags.py
$ cp temp/notifications/list.html collab/lib/python3.5/site-packages/notifications/templates/notifications/list.html
$ cp temp/notifications/settings.py collab/lib/python3.5/site-packages/notifications/settings.py
```
### Django-Wiki
```shell
$ cp temp/base_wiki.html collab/lib/python3.5/site-packages/wiki/templates/wiki/base.html
$ cp temp/article_menu_wiki.html collab/lib/python3.5/site-packages/wiki/templates/wiki/includes/article_menu.html
$ cp temp/article_wiki.html collab/lib/python3.5/site-packages/wiki/templates/wiki/article.html
```


## Optional(if the database is empty or using a new database):

Run the following command inside CollaborationSystem project

```shell
$ python3 manage.py migrate
$ python3 manage.py loaddata workflow
$ python3 manage.py loaddata roles
$ python3 manage.py loaddata faq

```

After migrations are done and all the tables are created, changes the body column in Articles tables to make it multilingual , will take symbols, unicode character etc.
do --

```shell
mysql -u root -p #and select the database that was created and run the following sql query
ALTER TABLE BasicArticle_articles MODIFY COLUMN body text CHARACTER SET utf8 COLLATE utf8_general_ci NULL;

```

Create an initial forum and set the permissions, also set the site ids
Create a admin user --

```shell
$ python3 manage.py createsuperuser

```

Goto - http://ipaddress/admin/ and use your admin user and password.

Find - MACHINA: FORUM and select Forums.

- Create a Forum (Add Forum) --

- Forum type = Default Forum

- Name = Collaboration System

- Description = “The forum for ‘Collaborative Communities’ will allow individual users to discuss on  communities, topics related to communities, and thus, enhance its value for the society in terms of education.”

And save the forum.

Cick on GLOBAL FORUM PERMISSIONS

- Under Edit group permissions
- Click on the search button and select author
- And click on Select button
- Set GRANTED permission on following options
    - Can read forum
    - Can see forum
    - Can delete own posts
    - Can edit own posts
    - Can post announcements
    - Can post stickies
    - Can post without approval
    - Can reply to topics
    - Can start new topics
- Save the permissions

Add Sites--

	Goto - http://ipaddress/admin/

Find - SITES and select Sites

Add all ip addresses and domain names (one at a time).
Keep the Domain name  and Display name same.
