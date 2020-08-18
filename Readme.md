# Redis for beginners
## What is Redis?
Redis stands for Remote Dictionary Server. It's an open source NoSQL in-memory database. 
It's a NoSQL database which means it doesn't use SQL structure for storing data. It's also an in-memory database which means Redis stores it data in RAM rather than in permanent storage like HDD or SSD. This means it is very fast as data read/write speed is very fast from RAM ,than from permanent storages.

## Redis in WSL(Ubuntu) userguide

### Installation
To install Redis in WSL(Windows Subsystem for Linux) we have to follow the steps below:

1. In the WSL terminal type `sudo apt get update` to update packages.
1. Then to install Redis we have to type `sudo apt install redis-server` .
1. To confirm the installtion we can type `redis-server --version`

Now to start the `redis-server` we have to type `sudo service redis-server start`
To access redis we have to type `redis-cli`
Now if we want to stop the `redis-server` we would have to type:
`sudo service redis-server stop`. We can also check if redis-server is properly running by giving the `ping` command in `redis-cli` and if the server is running properly it would return `PONG`.

We can also do `ECHO` command like,
```bash
ECHO 'Hi'
```
This should give back `Hi`.

To exit the `redis-cli` shell we would have to use `QUIT`

### Basic Commands

We can set a key value pair by using the `SET` command,
```
SET key value
```
It would be clear if we see an example, let's say we want to set a key `age` to the value 21, then we would have to type:
```
SET age 21
```
After setting the key, if we want to get the value we would have to use the `GET` command,
```
GET age
```
This would return the value that was set.

The value of a key could be a variety of thing,like it could be a string.
```
SET name 'Nissan'
```
If the value of a key is an integer we could use `INCR` command to **increment** the value.
Let's say the value of a key called `fps` is `60`. Then we can use the value by using the increment command,
```
INCR fps
```
After running this command if we do a `GET fps` we would see the value incremented to 61.

We can also decrement a value by using the `DECR` command. 
```
DECR fps
```
This would decrement the value of fps and if we do a get command we would see that the value of `fps` decremented to 60 from previous value of 61.

If we want to check if a key exists in our `resdi-server` we can use the `EXISTS` command like below,
```
EXISTS key
```
Let's say we want to know if a key named `fps` exists in our server.
So, we would type:
```
EXISTS fps
```
This command will return `1` if the key exists, otherwise it will return `0`.

We can delete a key value pair by using the `DEL`command.
```
DEL key
```
So, if we want to delet the `fps` key then we would use:
```
DEL fps
```
#### FLUSHALL
If we want to delete all the key value pairs in our redis-server then we can use the `FLUSHALL` command.
```
FLUSHALL
```
#### EXPIRE
If we want to set an expiration time to a key then we can use the `EXPIRE` command.
```
EXPIRE key time_to_live
```
After the time to leave has expired the key will be automatically deleted.

We can also see how much time is remaining until the key expires by using the `TTL` command. 