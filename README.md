Laravel WebSockets in PHP without Node.JS and Pusher service
======================

* ***Actions on the deployment of the project:***


- Making a new project dka-develop_laravel-php-websockets.loc:
	
	sudo chmod -R 777 /var/www/LARAVEL/VUE/dka-develop_laravel-php-websockets.loc

	//!!!! .conf
	sudo cp /etc/apache2/sites-available/test.loc.conf /etc/apache2/sites-available/dka-develop_laravel-php-websockets.loc.conf
			
	sudo nano /etc/apache2/sites-available/dka-develop_laravel-php-websockets.loc.conf

	sudo a2ensite dka-develop_laravel-php-websockets.loc.conf

	sudo systemctl restart apache2		

	sudo nano /etc/hosts
									
	cd /var/www/LARAVEL/VUE/dka-develop_laravel-php-websockets.loc


- Deploy project:

	git clone << >>
	
	_+ Сut the contents of the folder up one level and delete the empty one._

	composer install

- Create database, like dka-develop_laravel-php-websockets( `utf8mb4_general_ci` Collation )

- Configure database connection, `.env` file:

```		
BROADCAST_DRIVER=pusher
...
QUEUE_CONNECTION=sync
...
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
Фейковые данные:
...	
PUSHER_APP_ID=123
PUSHER_APP_KEY=123
PUSHER_APP_SECRET=1234324
```

- Reset cached settings:

	php artisan config:clear

- Run migrations:

	php artisan migrate

- Run Seeder: 

	php artisan db:seed
			
- !!!

	npm install

- !!!

	npm run dev

- Start websockets:

	php artisan websockets:serve		

- Start development server:

	php artisan serve		

[(11:20)]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=680 ) Checking the result:

	http://127.0.0.1:8000/
	
	http://127.0.0.1:8000/room/1

- _Launch 2 browser windows (- one window - private, to enter under different users):_

_!!! We go in each window under different users: !!! OPEN one window -> "Open a New Window", the second - "Open a New Private Window" !!!:_

`One window:`

	http://127.0.0.1:8000/

		`Login:`

			Vano  			
				vano_tatysho@gmail.com
				
				psw: vano_tatysho
														
`Second:`

	http://127.0.0.1:8000/			
	
		`Login:`
	
			Vaso
				vaso_nuasho@gmail.com
				
				psw: vaso_nuasho
																							
We enter the same room (- for example, the 1st) in both browsers:

	http://127.0.0.1:8000/room/1

![screenshot of sample]( https://github.com/mslobodyanyuk/dka-develop_laravel-php-websockets/blob/master/public/images/1.png )

#### useful links:

<https://www.youtube.com/watch?v=XkH1qR9TkA8&list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&index=9>

<https://dka-develop.ru/blog/article/laravel-websockets-na-php-bez-nodejs-i-servisa-pusher-besp-0403191710>

<https://github.com/dka-develop/laravel-php-websockets>

<https://www.youtube.com/watch?v=H_4UubWE9NQ&ab_channel=QiroLab>

---

[Laravel WebSockets на PHP без Node.JS и сервиса Pusher [ бесплатно, лайфхак, уроки laravel ] (13:06)]( https://www.youtube.com/watch?v=XkH1qR9TkA8&list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&index=9 )		

Description:

Let's run PHP websockets without Node.JS using the Laravel WebSockets package https: //github.com/beyondcode/laravel ...

- Introducing the beyondcode / laravel-websockets package
[0:00]( https://www.youtube.com/watch?v=XkH1qR9TkA8&list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&index=9 )

- Can this package be used without the pusher.com service?
[1:06]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=66 )

- 3 requirements so you can repeat the same experience
[1:36]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=96 )

- Why you need to read the description under the video
[3:17]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=197 )

- Demonstration of work on laravel-echo-server (Node.JS)
[3:48]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=228 )

- Beginning of porting to PHP
[5:36]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=336 )

- Demonstration of work
[11:14]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=674 )

- Route protection with dashboard
[12:32]( https://youtu.be/XkH1qR9TkA8?list=PLD5U-C5KK50WlQNiunPPXSj5jjxVVTPtk&t=752 )

Code from video and link to `GitHub` (on one page):

<https://dka-develop.ru/blog/article/laravel-websockets-na-php-bez-nodejs-i-servisa-pusher-besp-0403191710>

Ready project on `GitHub`:

<https://github.com/dka-develop/laravel-php-websockets>

The first step is to install the package using `composer`:

	composer require beyondcode/laravel-websockets
	
Next, you need to run the command that will create the migration file:

	php artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="migrations"
	
Running migrations, creating a table from a file with a migration:

	php artisan migrate
	
Create a configuration file for this package:

	php artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="config"

The next step is to register fake data for authorization with the `pusher` service:

```
\\ .env file
\\ Registers pusher as a broadcaster
BROADCAST_DRIVER=pusher
\\ Fake data
PUSHER_APP_ID=123
PUSHER_APP_KEY=123
PUSHER_APP_SECRET=1234324
```

Also, be sure to indicate here your domain name that you use for development and added to the file with hosts and registered in the web server:

```
\\ .env file
APP_URL=http://dkadevelop.dev
```

The next step is to go to the broadcasts config file `config/broadcasts.php`. In the key of the array with options to the `pusher` server, we write the following settings:

```
'host' => '127.0.0.1',
'port' => 6001,
'scheme' => 'http'
```

We enable sending events from clients in the `config/websockets.php` file:

	'enable_client_messages' => true,

Install two packages, this is `laravel-echo`, do not confuse with the server and the `pusher-js` library:

	npm install --save laravel-echo pusher-js

Do not forget that in laravel, starting from version 5.7, the structure of the folder with resources has changed. `resources/js/bootstrap.js`:

```html
	import Echo from 'laravel-echo'
	window.Pusher = require('pusher-js');

	window.Echo = new Echo({
    broadcaster: 'pusher',
    key: process.env.MIX_PUSHER_APP_KEY,
    cluster: process.env.MIX_PUSHER_APP_CLUSTER,
    wsHost: window.location.hostname,
    wsPort: 6001,
});
```

Be sure to re-collect our changes:

	npm run dev
	
Also, be sure to reset the cache:

	php artisan config:cache
	
The following command is used to run on the server side:

	php artisan websockets:serve
	
Ready project on `GitHub`:

<https://github.com/dka-develop/laravel-php-websockets>
