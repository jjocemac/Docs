# Deploying Python Flask apps on Heroku

- Headed over to www.heroku.com and signed up
- Installed pipenv (on foe-linux):
```
module load python3 python-libs
pip install pipenv --user
```
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

## 'hello world' app
- Created a 'hello world' flask app and added to github here: https://github.com/jjocemac/flask-hello-world.git
