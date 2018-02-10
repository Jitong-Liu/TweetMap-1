# Real-time Twitter Sentiment Visualization

![image](https://github.com/Jitong-Liu/TweetMap-1/blob/master/images/markers.png)
![image](https://github.com/Jitong-Liu/TweetMap-1/blob/master/images/heatmap.png)
![image](https://github.com/Jitong-Liu/TweetMap-1/blob/master/images/sentiment.png)

## Architecture
![image](https://github.com/Jitong-Liu/TweetMap-1/blob/master/images/architecture1.png)

### Streaming

* Reads a stream of tweets from the Twitter Streaming API
* After fetching a new tweet, check to see if it has geolocation info and is in English.
* Once the tweet validates these filters, send a message to Kafka for asynchronous processing on the text of the tweet

### Worker

* A worker pool that will pick up messages from the queue to process.
* Make a call to the sentiment API to calculate polarity of each tweet.
* As soon as the tweet is processed send a notification ­using SNS­ to an my backend.

### Backend

* On receiving the notification, index this tweet in Elasticsearch.
* The backend provide the functionality to the user to search for tweets that match a particular keyword.

### Frontend

* Give the user the ability to search your index via a free text input.
* Plot the tweets that match the query on a map.
* Lastly, use D3.js to indicate the sentiment analysis.
