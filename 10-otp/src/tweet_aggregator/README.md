# TweetAggregator

Distributed Tweet Aggregator


## Nodes

- GateKeeper
- Aggregator
- Search.Client


## Example Usage

### 1. Export required envorinment vairables for GateKeeper to make OAuth requests

```bash
$ touch .env

# .env
export TWEET_CONSUMER_KEY=...
export TWEET_CONSUMER_SECRET=...
export TWEET_ACCESS_TOKEN=...
export TWEET_ACCESS_TOKEN_SECRET=...
```


### 2. Start Aggregator / GateKeeper node

```bash
iex --name aggregator@127.0.0.1 -S mix
iex(aggregator@127.0.0.1)1> TweetAggregator.become_leader
:yes
```

 ### 3. Start client search node(s)

```bash
iex --name client1@127.0.0.1 -S mix
iex(client1@127.0.0.1)1> Node.connect :"aggregator@127.0.0.1"
true
iex(client1@127.0.0.1)2> TweetAggregator.Search.Client.poll(:client1, ["elixir"], [])
New results
Client: Got 1 result(s)
```

### 4. Watch Aggregator notifications on Aggregator node

```
>> client1
@noctarius2k: Elixir - The Ruby like Erlang VM Language http://t.co/FzCeytAv5t
```


