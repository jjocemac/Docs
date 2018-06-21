# Deploying Python Flask apps on Heroku

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
- Installed pipenv (on foe-linux):
```
module load python3 python-libs
pip install pipenv --user
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
- Set up and run a database:
```
mkdir -p postgres/data
initdb -D ~/postgres/data/
postgres -D ~/postgres/data/
```
- In another shell, connected to the db:
```
~/SW/postgres/bin/psql -U earjjo postgres
```

## 'hello world' app
- Created a 'hello world' flask app and added to github here: https://github.com/jjocemac/flask-hello-world.git
