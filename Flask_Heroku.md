# Deploying Python Flask apps on Heroku

## Setup

- Headed over to www.heroku.com and signed up
- Downloaded the Heroku CLI binaries (on foe-linux):
```
cd ~/SW
wget https://cli-assets.heroku.com/heroku-linux-x64.tar.gz
tar -xzvf heroku-linux-x64.tar.gz
rm heroku-linux-x64.tar.gz
```
- Added heroku bin path to `~/.bashrc` file and source:
```
export PATH="/nfs/see-fs-01_users/earjjo/SW/heroku/bin:${PATH}"
```
- Logged into heroku:
```
heroku login
```

- Installed pip3 and pipenv (on foe-linux):
```
cd ~/Downloads
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py --user
rm get-pip.py
~/.local/bin/pip3 install pipenv
```

- (Used https://www.endpoint.com/blog/2013/06/12/installing-postgresql-without-root for below)
- Downloaded postgresql-10.4.tar.gz from https://www.postgresql.org/ftp/source/v10.4/ and installed (on foe-linux):
```
module load python3 python-libs
cd ~/Downloads
tar -xzvf postgresql-10.4.tar.gz
cd postgresql-10.4
mkdir ~/SW/postgres
./configure --prefix=$HOME/SW/postgres/ --with-python
make -j 4
make install
rm -rf postgresql-10.4*
```
- Added postgres bin path to `~/.bashrc` file and source:
```
export PATH="/nfs/see-fs-01_users/earjjo/SW/postgres/bin:${PATH}"
```
- To set up and run a database:
```
mkdir -p postgres/data
initdb -D ~/postgres/data/
postgres -D ~/postgres/data/
```
- To connect to the DB, in another shell:
```
psql -U earjjo postgres
```

## 'Hello world' app
- Created a 'hello world' flask app and added to github here: https://github.com/jjocemac/flask-hello-world.git
- Repo includes a file called `Procfile` with one line of code:
```
web: gunicorn hello:app --log-file -
```
- Created a python3 pipenv within the repo main directory, installed the dependencies and added pipfiles to the git repo:
```
~/.local/bin/pipenv --three install
~/.local/bin/pipenv shell
~/.local/bin/pipenv install flask gunicorn
git add Pipfile Pipfile.lock
git commit -m "Add pipfiles"
git push
```
- Tested app runs:
```
python hello.py
```
- Create heroku app and launch:
```
heroku create
git push heroku master
heroku open
```
- To stop the app, type (from inside main dir):
```
heroku ps:scale web=0
```
- To relaunch the app, type (from inside main dir):
```
heroku ps:scale web=1
```
