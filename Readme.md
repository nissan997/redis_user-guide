# Redis for beginners
## What is Redis?
**Redis** stands for Remote Dictionary Server. It's an open source NoSQL in-memory database. 
It's a NoSQL database which means it doesn't use SQL structure for storing data. It's also an in-memory database which means Redis stores it data in RAM rather than in permanent storage like HDD or SSD. This means it is very fast as data read/write speed is very fast from RAM ,than from permanent storages.
It's frequently used as caching server. 

## What is Redis Cluster?

Redis cluster is a strategy used with Redis. In a Redis cluster there are a few master and a few slave. To be precise there should be :
1. Minimum of 3 Redis master nodes.
1. Minimum of 3 slave, each for every master.

Now there's a reason why minmum 3 master is needed, because the master and slave nodes communicates with one another using a protocol called `Gossip Protocol`. If a node fails other nodes have to come in concensus with each other. If max number of node votes that a node is failing then they will ignore that node.

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
```
TTL key
```

We can also set `TTL` when creating a new key using the command `SETEX`.
```
SETEX key time_to_live value
```
The `SETEX` command is the combination of `SET` and `EXPIRE` command .
Now let's say we created a key with TTL but now we don't want the key to be expired, then we can use the `PERSIST` command,
```
PERSIST key
```
We can set more than one key value pair using the `MSET` command.
```
MSET key1 value1 key2 value2
```
We can append values to a key using the `APPEND` command.
```
APPEND key value
```
`APPEND` doesn't replaces the value of the key it just appends to it or in other words add the new value to the old value.
Let's say we have a key called **name** which has a value of "Nissan" now we want to append " Devnath" to the **name** value, then we can type:
```
APPEND name " Devnath"
```
After giving this command if we `GET` the value of the **name** key, then we can see that the value would be "Nissan Devnath".

We can rename a key using the command `RENAME` .
```
RENAME old_key_name new_key_name
```

### Redis List

We can store data as list in Redis using the `LPUSH` and `RPUSH` command. The difference between `LPUSH` and `RPUSH` is that `LPUSH` inserts the new data at the start of the list and `RPUSH` inserts the new data at the end of the list.

We can use the `LPUSH` and `RPUSH` command like below:
```
LPUSH list_name values
RPUSH list_name values
```
We can query the values in a list using `LRANGE` command.
If we want all the values in a list we have to type:
```
LRANGE list_name 0 -1
```
We can also get the values between two index.
```
LRANGE list_name start_index stop_index
```
Now if we want to get the length of the list then we can use the `LLEN` command.
```
LLEN list_name
```
We can pop items of the list. Poping items from list means that we will get the value from the start or end of the list and the value will also be removed.
There are two pop commands `LPOP` and `RPOP`. `LPOP` removes the first element of the list and `RPOP` removes the last element of the list. 
```
LPOP list_name
RPOP list_name
```
We can insert new values to the list before or after specific values using the `LINSERT` command. 
If we want to insert a new value "sayem" before the value "nissan" then we would have to type:
```
LINSERT list_name BEFORE "nissan" "sayem"
```
We can also use the `AFTER` with the `LINSERT` command to insert a new value after a specific value.
```
LINSERT list_name AFTER "nissan" "sajib"
```
After running this command the value "sajib" will be inserted after "nissan" . The list will be "sayem" "nissan" "sajib" after running the above insert commands.

