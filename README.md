# Level0_Webapp
Simple CRUD website using Yii2 Framework (MVC)

## Dependencies 
You need to have a LAMP or WAMP server.

## We'll cover following Steps  
I will demonstrate basic steps for Ubuntu operating system.

1. Installing LAMP (Only ubuntu will be covered, you can skip this step if you already have LAMP or WAMP server)
2. Intalling Yii2 Framework (We will composer for the same)
3. Building database for your CRUD application. 
4. Connecting your database with Yii2
5. Using Gii for generating CRUD 

> Let dive onto each of this one by one

[1]: https://wiki.debian.org/tasksel "Tasksel"
## Installing LAMP on Ubuntu
We're going to use tasksel for achieving this Installation which is provided by ubuntu itself, [Tasksel][1] is fast and installs the entire in one hit, So lets install __tasksel__ first  
 `sudo apt-get install tasksel`
 
 Once this process is finished, you need to use __tasksel__ to install __lamp-server__, here is how we have to do that 
 `sudo tasksel install lamp-server`
 This process can ask you setting your database password multiple times, you must enter the same everytime. Once this process is finished, You need to go to browser and type __localhost__ and You must see a __Apache2 Default ubuntu page__.
 
 _Note: Make sure you dont have any other service running on Port 80_ 
 
 ## Installing Yii2 Framework 
 This might be most tricky process of all. There are plenty of ways available to install Yii2. But We will be using __composer__ which is a Package Manager for PHP on top of that Yii2 works. You can use the following commands to install composer
 `curl -sS https://getcomposer.org/installer | php`
 Above command will Install __composer__ for you but this is available only for your local directory, In order to make it global you should type the following command 
 `mv composer.phar /usr/local/bin/composer` 
 This will make your __composer__ globally accessible. 
 
 __Important: If you're installing composer for the first time, your terminal will ask you to paste a Token from github which you can get by link, that your terminal asked to go on and get the token__ 
 
 _Note: If you already have composer installed on your ubuntu system you can ignore this step._
 
 Once __composer__ is installed we can begin with install Yii2 Framework with the following commands, But First make sure you're with in a web accessible directory which is _/var/www/html_ as per Ubuntu and LAMP if everything is running of default configuration. Lets start the Yii2 Installation
 
 `composer global require "fxp/composer-asset-plugin:^1.2.0"`
  This is an essential plugin which is required by Yii2 So if you are moving your Yii2 web app from one system to another you might need to install this plugin on that system too. And the next command will actually install the Yii Framework for you.
  `composer create-project --prefer-dist yiisoft/yii2-app-basic your_directoy_name`
  
_Note: __your_directory_name__ can be anyname this is going to be your webApp directory._
This process is going to take a while depending on your internet speed. Once the process is completed you must be able to see your app working on the address _http://localhost/your_directory_name/web/index.php 

## Building Database for your application 
In order create database for your application type the following command on Ubuntu Terminal
`mysql -u root -p` 
You need to enter your password that you created while installing LAMP. You might not see asteriks while typing but its working. Hit Enter! once you are connected you will be inside mysql shell which shows something like __mysql>__ Now you have to create a database that can be done by 
`CREATE DATABASE yii2Test;` 
Now you need to select the database in order to work on the same database. 
`USE yii2Test` 
Lets create a table that we will be using in Yii2 
```
CREATE TABLE Persons (
    PersonID int Primary Key,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
); 
```
## Connecting your database to yii2 Application
To connect with your database you must edit the file _your_directory_name/config/db.php_. Below is the content of that file 
```return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=localhost;dbname=yii2Test',
    'username' => 'root',
    'password' => 'your_password',
    'charset' => 'utf8',
];
```
Most probably your password field will be empty, So you need to provide you MySQL password here in place of _your_password_ that you had set while installing LAMP server. Database name should be this only if you are following the document or if you have created your own database with a different name, then replace _yii2Test_ with your database name. Once you have edited this file you are already connected to your database.

## Using Gii for CRUD application
Open your browser and go to the url _http://localhost/your_directory_name/web/index.php?r=gii_ you must see a webpage that says __Welcome to Gii__ in big font, There you should see a sub heading called __MODEL GENERATOR__ click on the _start_ button below that heading, We need to tell to our APP how our table look likes in order to CRUD over that table. Once the link is opened you must see a small form. 

The First Field is Table Name, yes exactly you need to just provide the name of table (Case sensitive) that you have just created i.e. _Persons_ And thats all. Go extreme down the bottom of the page you must see a button _Preview_ Click on that, you will land on the similar looking page with a extra button just near to _Preview_ i.e. _Generate_ Hit the generate button 

_Note: If the Generate button gives you a permission error then type in terminal `sudo chmod 777 -R /var/www/html/your_directory_name/models` and repeat the __MODEL GENERATOR__ Process._

If the process is completed successfully you will see the following message in green block _The code has been generated successfully._

Now We're almost done. Lets generate CRUD now, browse again the same gii url i.e. _http://localhost/your_directory_name/web/index.php?r=gii_ You might have already noticed the other heading as __CRUD GENERATOR__ click on the _start_ button below that heading, Now the form that you see is bit bigger than the former one So there are 3 required fields that we must fill give the value written in _italics_
* Model Class: _app\models\Persons_
* Search Model Class: _app\models\PersonsSearch_
* Controller Class: _app\controllers\PersonsController_ 

_Note: Everything is case sensitive here_ 

Now, we need to again click on _preview_ button, and Thereafter _generate_ button if it again shows the permisson error just repeat the `chmod` command for _/var/www/html/your_directory_name/controllers/_ and _/var/www/your_directory_name/views/_ and Repeat the process. Once it is successfully completed we have our application ready. 

## Congrats
Head over to the browser and type _http://localhost/your_directory_name/web/index.php?r=persons_, now you can create the data and every other operation related to CRUD. 
