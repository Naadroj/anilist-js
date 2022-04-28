# anilist-js

## Build Setup

```bash
# install dependencies
$ yarn install

# build for production and launch server
$ yarn build
$ yarn start

```

## HELP

```bash
# if you already have something running on localhost:3000
# on Linux
$ sudo kill -9 `sudo lsof -t -i:3000`
# on windows
$ netstat -ano | findstr :3000
# on MacOs
$ sudo lsof -i :3000 
    # get PID and then kill the process
$ kill -9 <PID>

```


# build dev with hot reload (only for development)
$ yarn dev