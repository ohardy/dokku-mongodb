# MongoDB plugin for Dokku

Project: https://github.com/progrium/dokku

## Installation

```
cd /var/lib/dokku/plugins
git clone https://github.com/ohardy/dokku-mongodb mongodb
dokku plugins-install
```


## Commands
```
$ dokku help
    mongodb:console     <app>               Launch a MongoDB console for a given app
    mongodb:env         <app>               Get generated environment variables for <app>
    mongodb:url         <app>               Get DATABASE_URL for <app>
    mongodb:create      <app>               Create a MongoDB database
    mongodb:delete      <app>               Delete specified MongoDB database
    mongodb:link        <app> <another_app> Give environment variable of database of <app> to <another_app>
    mongodb:unlink      <another_app>       Unlink <another_app> to a database
    mongodb:dump        <app> > <filename>  Dump database to SQL format
    mongodb:restore     <app> < <filename>  Restore database from SQL format
    mongodb:admin_console                   Launch a MongoDB console as admin user
    mongodb:restart                         Restart the MongoDB docker container and linked app
    mongodb:start                           Start the MongoDB docker container if it isn't running
    mongodb:stop                            Stop the MongoDB docker container
    mongodb:status                          Shows status of MongoDB
    mongodb:list                            List all databases
    mongodb:update                          Update this plugin
    mongodb:migrate                         Migrate
```

## Updating this plugin
Dokku doesn't handle plugin update. I made a pull request to dokku for that (https://github.com/progrium/dokku/pull/669)

So, each time you update this plugin with `git pull`, you need to call:
```
$ dokku mongodb:migrate
```

## Info
This plugin adds following environment variables to your app automatically:

* DATABASE_URL
* DB_HOST
* DB_PORT
* DB_NAME
* DB_USER
* DB_PASS

## Usage

### Start MongoDB:
```
$ dokku mongodb:start                 # Server side
..or..
$ ssh dokku@server mongodb:start      # Client side

```

### Stop MongoDB:
```
$ dokku mongodb:stop                 # Server side
..or..
$ ssh dokku@server mongodb:stop      # Client side

```

### Restart MongoDB:
```
$ dokku mongodb:restart                 # Server side
..or..
$ ssh dokku@server mongodb:restart      # Client side

```

### Create a new database:
```
$ dokku mongodb:create foo            # Server side
..or..
$ ssh dokku@server mongodb:create foo # Client side
```

### Dump database to SQL:
```
$ dokku mongodb:dump foo > filename.sql # Server side
..or..
$ ssh dokku@server mongodb:dump foo > filename.sql # Client side
```

### Restore database from SQL:
```
$ dokku mongodb:restore foo < filename.sql # Server side
..or..
$ ssh dokku@server mongodb:restore foo < filename.sql # Client side
```

### Copy database foo to database bar using pipe:
```
$ dokku mongodb:dump foo | dokku mongodb:restore bar # Server side
```


## Link
You can link a database to an application :

- Create database:
```
$ dokku mongodb:create foo
```
- Push another_app to dokku and link it to foo with:
```
$ dokku mongodb:link foo another_app
```
- Environment variables for database foo will be available in another_app

## Unlink
```
$ dokku mongodb:unlink another_app # Server side
```
