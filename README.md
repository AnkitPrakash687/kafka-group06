# Kafka-group06

## Introduction
Twitter provide the free stream data for various business analytics. In this project we will stream the twitter data using Apache Kafka which is a streaming platform. These data can be useful for creating trending topics in the various fields. 

We will be setting up a kafka twitter stream using python libraries

## Prerequisites

We assume that:
* you have python installed and have a basic knowledge how it looks like.
* you are aware how to run zookeeper server.
* you are aware how to run kafka server.
* you have twitter developer account. (If you don't have the developer account, [click here to know more](https://docs.inboundnow.com/guide/create-twitter-application/))

## Steps to follow:

1. Create an App on the Twitter API website. Copy all the keys and token of your app.
2. Install kafka-python and twitter-python with below commands
    ```
    pip install kafka-python
    pip install python-twitter
    pip install tweepy   
    ```
3. Start Zookeeper and Kafka.

```
./zkServer.cmd
./kafka-server-start.bat .\server.properties
```

4. Create a topic.Example: "linkin park" or "Climate Change"
```
./kafka-topics.bat --zookeeper localhost:2181 --create  --replication-factor 1 --partitions 1 --top
ic linkin
```

5. Copy the below code. Replace the variable code with your twitter keys:

```
  from tweepy.streaming import StreamListener
  from tweepy import OAuthHandler
  from tweepy import Stream
  from kafka import SimpleProducer, KafkaClient

  access_token = "(get your own)"
  access_token_secret =  "(get your own)"
  consumer_key =  "(get your own)"
  consumer_secret =  "(get your own)"

  class StdOutListener(StreamListener):
    def on_data(self, data):
        producer.send_messages("trump", data.encode('utf-8'))
        print (data)
        return True
    def on_error(self, status):
        print (status)

  kafka = KafkaClient("localhost:9092")
  producer = SimpleProducer(kafka)
  l = StdOutListener()
  auth = OAuthHandler(consumer_key, consumer_secret)
  auth.set_access_token(access_token, access_token_secret)
  stream = Stream(auth, l)
  stream.filter(track="linkin park")
```
6. Run the above python code.
7. You can test that topics are getting published in Kafka by using
```
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic linkin --from-beginning
```

## References
https://www.bmc.com/blogs/working-streaming-twitter-data-using-kafka/

