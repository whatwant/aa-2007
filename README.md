# aa-2007
Associate Architect


## Install

- based on Ubuntu 18.04 LTS

### Node.JS

- reference
  - https://soojae.tistory.com/25

- install
```
$ sudo apt install curl build-essential
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
$ sudo apt install nodejs
```

- check
```
$ node -v
```

### MongoDB

- reference
  - https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

- install
```
$ wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
$ echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
$ sudo apt update
$ sudo apt install -y mongodb-org
```

- run
```
$ sudo systemctl start mongod
```

- check
```
$ sudo systemctl status mongod
```
