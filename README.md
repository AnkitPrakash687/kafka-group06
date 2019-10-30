# kafka-group06

## Introduction

## Prerequisites

We assume that:
* you have python installed and have a basic knowledge how it looks like.
* you are aware how to run zookeeper server.
* you are aware how to run kafka server.

## Steps to follow:

1. Create an App on the Twitter API website. Copy all the keys and token of your app.
2. Install kafka-python and twitter-python with below commands
    ```
    pip install kafka-python
    pip install python-twitter
    pip install tweepy
    
    ```
3. Start Zooper and Kafka
4. Create a topic.Example: "linkin park" or "Climate Change"
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

