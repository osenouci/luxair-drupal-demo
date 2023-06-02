# Summary
The aim of this project to explain the complexity that a Drupal developer faces at Luxair. 

The project contains two disconnected applications. The first is a `Drupal application` that runs inside a Docker container.While the second application is a `Signle page application` powered by Angular.

A recurring developement task consists of:

1. Importing a SPA application so that is displayed inside a Drupal page.
2. Using the Drupal backend to customize the SPA application.



The aim of this task is to check if you are able to carry out the task. Here are the steps required to import the SPA and use Drupal to configure it:
1. Create a custome module in order to import the SPA's assests.
1. Use the custome module to create an `entity` that the content manager will use to create a page containing the SPA and configure it.
1. Create a theme that will modify the `entity`'s view and inject `<app-root></app-root>` into it.


## Running the Drupal application
___
A docker compose file has been provided. One way of running the project is to use `docker` and `docker compose`. Another way is to install LAMP stack locally and run the project.

### Running the project using Docker

1. Pull the images
```
docker compose pull
```

2. Create and run the containers
```
docker compose start
```

### Drupal installation 

1. Open `http://localhost:8080/` in a browser
1. Select english as a language
1. Select the standard installation profile
1. Configure the data connectivity as follows:
    1. **Database type**: `MySQL, MariaDB, Percona Server, or equivalent`
    1. **Database name**: `drupal`
    1. **Username**: `drupal_database_user`
    1. **Password**: `drupal_database_password`
    1. Select `mysql` as **host** from the *Advanced options*


**Drupal url**
```
http://localhost:8080
```

**Admin section url**
```
http://localhost:8080/login
```

## Useful Drush commands 
____

**Install drush inside the container**
```
export COMPOSER_MEMORY_LIMIT=-1
composer require --dev drush/drush:10.x
```

**Install the module**
```
vendor/bin/drush en module_name
```

**Remove a module**
```
vendor/bin/drush pm:uninstall module_name
```