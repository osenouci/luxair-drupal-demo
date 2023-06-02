# Summary
The aim of this project to explain the complexity that a Drupal developer faces at Luxair. 

The project contains two disconnected applications. The first is a `Drupal application` that runs inside a Docker container. While the second application is a `Signle page application` powered by Angular.

The two will be used to demo a recurring developement task that consists of:
1. Importing a SPA application so that it is displayed inside a Drupal page.
2. Using the Drupal backend to customize the SPA application.

> **Our goal**
>
> Our aim is to estimate the required effert to support Drupal as a developer.
> The solution of the problem is provided as a separate branch titled `solution-branch`.
>
> Please consider the problem and see if know how to solve it without necessarly coding it. If the solution is not clear than look at the solution branch.


## Work flow to be considered
___
We will create an **advert** module that will be used to create a base `content-type`. The **advert** `content-type` will be used by content managers to create customizable pages where they can customize the attributes of the single page application. Currently we pass a single value called `range`. This value is the equivalent of the `skip` in pagination terms.

The work flow of a content manager that wants to install and use the `advert` content is as follows:

1. When we visit the content types section located under the `structure` tab, we should have a list of default **content types**.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-21-54.png "Title")

2. In ordert to add our new adverting content type, we install the Advert module that we have created. The advert module does the following:

    1. Imports our `Single Page Application` as a library.
    1. Attaches the `Single Page Application` assets to the page source.
    1. Creates an `Advert` content type.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-22-40.png "Title")

3. Once we install the advert module, a new `Advert` content type should appear under the `structure` tab.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-23-11.png "Title")

4. We create a test page of type `advert` by going to Content and then clickig on the `+Add content` button.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-34-53.png "Title")

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-35-04.png "Title")

5. We fill down the form with test data like shown here below and finally preview the changes and save them.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-35-21.png "Title")

6. Drupal will render our new page. It will not contain our Angular app as the html does not contain the `<app-root>` tag

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-35-39.png "Title")

7. We need to overwrite the view of the `advert` page in order to render the JavaScript application and also pass it the value of the `product range` field. I have created a new theme called `Advert theme` to do this. 
The theme can be installed using the appearance tag.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-36-06.png "Title")

8. Refresh the advert page from `step 6` and it will render the angular application correctly.

![alt text](./screenshots/Screenshot%20from%202023-06-02%2016-36-39.png "Title")

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


## Notes on CROS requests
____

The single page application makes cross domain requests which are blocked by our CORS policies. For demo purposes disable chrome's security. 

To disable the chrome security on Linux, use the following command:

```
/usr/bin/google-chrome --disable-web-security --ignore-certificate-errors  --disable-gpu --user-data-dir=/tmp/chrome
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