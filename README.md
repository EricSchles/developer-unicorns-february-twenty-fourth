#Building Web Apps Fast
##Flask,Heroku, Syncano

###Heroku

Setting up Heroku:

#####Installin' Stuf'

* [Get a free account](https://signup.heroku.com/dc)
* [Download the toolbelt](https://devcenter.heroku.com/articles/getting-started-with-python#set-up)
* `heroku login` - only required the first time you create a heroku app for verification purposes

#####Figurin' to Configure some things

* create a `requirements.txt` file --> `pip freeze > requirements.txt` 
	* Unless you are on ubuntu.  Then run [this pruner](https://github.com/EricSchles/requirements_pruner_heroku) after you do `pip freeze > requirements.txt`
	* Or make sure you set up a virtualenv and use the pip within your virtualenv
* create a Procfile
	* For most simple web apps you'll only need: `web: gunicorn app:app`
		* in general Procfile's have the following form: <process type> : <command>, for more info [check this out](https://devcenter.heroku.com/articles/procfile)	
	* For more advance web apps check out the [foreman reference](http://ddollar.github.io/foreman/) and [an interesting example with web sockets](https://devcenter.heroku.com/articles/python-websockets)
	* concurrency with foreman:
		* Procfile: 
			
			``` 
			  web: gunicorn web:web
		          worker: python scraper.py 
			```
		* terminal command: `foreman start -c web=1, worker=2`

* create a `runtime.txt` file
	* file contents: `python-2.7.6` 
	* There is a known bug with gevent and python-2.7.9 that breaks ssl.

#####Terminal time

* push your project up to git:
	* `git init`
	* `git add -A`
	* `git commit -a -m "first commit"`
	* `git remote add origin git@github.com:[user-name]/[repo name].git`
	* `git push -u origin master`

* push your project to heroku:
	* `git push heroku master`
	* `heroku ps:scale web=1`
	* `heroku open`

###Syncano

* setting environment variables - locally
	* Ubuntu - edit .bashrc (you can get there by typing `cd ~`)
	* set instance name: 	
	    `export SYNCANO_INSTANCE_NAME=[instance name]` AND 
		`export PATH="$SYNCANO_INSTANCE_NAME:$PATH"` 
		to the end of the file.
	* set api key:
		`export SYNCANO_API_KEY=[api key]` AND 
		`export PATH="$SYNCANO_API_KEY:$PATH"` 
		to the end of the file.

*  setting environment variables - on heroku:
	*  `heroku config:set SYNCANO_INSTANCE_NAME=[instance name]`
	*  `herok config:set SYNCANO_API_KEY=[api key]`

###Flask

* routes:
	* Example:
		```
			from flask import Flask
			app = Flask(__name__)
		
			@app.route("/")
			def index():
				return 'Hello world'
		```
	* @app.route -> sets the route relative to the base url.

* redirects, render_template, url_for  
	* Example:
	
		```
			
			from flask import Flask
			app = Flask(__name__)
			
			@app.route("/")
			def index
		```