# Deploying Python Flask apps on Heroku

- Headed over to www.heroku.com and signed up
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
- Set up and run a database:
```
mkdir -p postgres/data
~/SW/postgres/bin/initdb -D ~/postgres/data/
~/SW/postgres/bin/postgres -D ~/postgres/data/
```
- In another shell, connect to the db:
```
~/SW/postgres/bin/psql -U earjjo postgres
```

## 'hello world' app
- Created a 'hello world' flask app and added to github here: https://github.com/jjocemac/flask-hello-world.git
