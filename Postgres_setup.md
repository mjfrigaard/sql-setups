# PostgreSQL application and setup

Download the application from [this](https://postgresapp.com/) website and follow the installation instructions. 

## First steps 

In the terminal, enter the following:

```
sudo mkdir -p /etc/paths.d &&
echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
```

You'll be asked to enter whatever password you need to install programs on your computer. 

## Create users

[documentation](http://postgresguide.com/setup/users.html)

Now we can create a user. In a new terminal session (restart terminal after entering the previous commands), enter the following. 

```
psql -h localhost
```

This will bring up the psql command line. 

```
psql (10.5)
Type "help" for help.

martinfrigaard=# 
```

To create a user for myself, I enter a user name and password.

```
CREATE USER martin WITH PASSWORD '%LWGma9c';
```

