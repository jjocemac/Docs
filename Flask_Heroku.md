# Deploying Python Flask apps on Heroku

## Setup

- Headed over to www.heroku.com and signed up
- Downloaded the Heroku CLI binaries (on foe-linux):
```sh
$ cd ~/SW
$ wget https://cli-assets.heroku.com/heroku-linux-x64.tar.gz
$ tar -xzvf heroku-linux-x64.tar.gz
$ rm heroku-linux-x64.tar.gz
```
- Added heroku bin path to `~/.bashrc` file and source:
```sh
export PATH="/nfs/see-fs-01_users/earjjo/SW/heroku/bin:${PATH}"
```
- Logged into heroku:
```sh
$ heroku login
```

- Installed pip3 and pipenv (on foe-linux):
```sh
$ cd ~/Downloads
$ wget https://bootstrap.pypa.io/get-pip.py
$ python3 get-pip.py --user
$ rm get-pip.py
$ ~/.local/bin/pip3 install pipenv
```

- (Used https://www.endpoint.com/blog/2013/06/12/installing-postgresql-without-root for below)
- Downloaded postgresql-10.4.tar.gz from https://www.postgresql.org/ftp/source/v10.4/ and installed (on foe-linux):
```sh
$ module load python3 python-libs
$ cd ~/Downloads
$ tar -xzvf postgresql-10.4.tar.gz
$ cd postgresql-10.4
$ mkdir ~/SW/postgres
$ ./configure --prefix=$HOME/SW/postgres/ --with-python
$ make -j 4
$ make install
$ rm -rf postgresql-10.4*
```
- Added postgres bin path to `~/.bashrc` file and source:
```sh
export PATH="/nfs/see-fs-01_users/earjjo/SW/postgres/bin:${PATH}"
```
- To set up and run a database:
```sh
$ mkdir -p postgres/data
$ initdb -D ~/postgres/data/
$ postgres -D ~/postgres/data/
```
- To connect to the DB, in another shell:
```sh
$ psql -U earjjo postgres
```

## 'Hello world' app
- Created a 'hello world' flask app and added to github here: https://github.com/jjocemac/flask-hello-world.git
- Repo includes a file called `Procfile` with one line of code:
```
web: gunicorn hello:app --log-file -
```
- Created a python3 pipenv within the repo main directory, installed the dependencies and added pipfiles to the git repo:
```sh
$ ~/.local/bin/pipenv --three install
$ ~/.local/bin/pipenv shell
$ ~/.local/bin/pipenv install flask gunicorn
$ git add Pipfile Pipfile.lock
$ git commit -m "Add pipfiles"
$ git push
```
- Tested app runs:
```sh
$ python hello.py
```
- Create heroku app and launch:
```sh
$ heroku create
$ git push heroku master
$ heroku open
```
- To stop the app, type (from inside main dir):
```sh
$ heroku ps:scale web=0
```
- To relaunch the app, type (from inside main dir):
```sh
$ heroku ps:scale web=1
```
- To get an interactive bash shell on the Heroku dyno that is running the app:
```sh
$ heroku run bash
```

## Heroku's 'python-getting-started' app
- Get repo:
```sh
$ cd ~/gitRepos
$ git clone https://github.com/heroku/python-getting-started.git
$ cd python-getting-started
```
- To deploy on Heroku:
```sh
$ heroku create
$ git push heroku master
$ heroku run python manage.py migrate
$ heroku open
```
- To run the app locally ***CURRENTLY DOESN'T WORK***:
```sh
$ ~/.local/bin/pipenv --three install
$ ~/.local/bin/pipenv shell
$ export DATABASE_URL=postgres://$(whoami)
$ createdb python_getting_started
$ python manage.py migrate
$ python manage.py collectstatic
$ heroku local
```

## [This](https://medium.com/the-andela-way/deploying-a-python-flask-app-to-heroku-41250bda27d0) heroku+flask+postgreSQL app
- Get repo:
```sh
$ cd ~/gitRepos
$ git clone https://github.com/heroku/python-getting-started.git
$ cd bucket_api_heroku
```
- Set up venv and Procfile:
```sh
$ ~/.local/bin/pipenv --three install
$ ~/.local/bin/pipenv shell
$ ~/.local/bin/pipenv install gunicorn
$ echo 'web: gunicorn app:app' > Procfile
$ git rm requirements.txt
$ git add -A
$ git commit -m "Pip and Proc files"
```
- Heroku steps:
```sh
$ heroku create
$ git push heroku master
```
