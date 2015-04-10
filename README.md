## Description
A Twitter Node Module to authenticate and interact with the Twitter API from NodeJS. 

## Installation
```	
npm install twitter-js-client
```
```javascript
var Twitter = require('twitter-js-client').Twitter;
```
## Usage
You need to create a [Twitter app](https://dev.twitter.com/apps) to use the API. 

```javascript
	//Callback functions
	var error = function (err, response, body) {
    	console.log('ERROR [%s]', err);
	};
	var success = function (data) {
    	console.log('Data [%s]', data);
	};

	var Twitter = require('twitter-js-client').Twitter;

	//Get this data from your twitter apps dashboard
	var config = {
    	"consumerKey": "XXX",
    	"consumerSecret": "XXX",
    	"accessToken": "XXX",
    	"accessTokenSecret": "XXX",
    	"callBackUrl": "XXX"
	}

    var twitter = new Twitter(config);
	
	//Example calls
	twitter.getUserTimeline({ screen_name: 'BoyCook', count: '10'}, error, success);
	twitter.getMentionsTimeline({ count: '10'}, error, success);
	twitter.getHomeTimeline({ count: '10'}, error, success);
	twitter.getReTweetsOfMe({ count: '10'}, error, success);
	twitter.getTweet({ id: '1111111111'}, error, success);

	twitter.getSearch({'q':'#elections #greenparty','locale':'ja','count': 100}, error, success);

```

Twitter has a comprehensive [REST api](https://dev.twitter.com/rest/public) if you need to use something that doesn't have a wrapper function in the library call it directly : 
```javascript
	twitter.getCustomApiCall('/statuses/lookup.json',{ id: '412312323'}, error, success);
	twitter.postCustomApiCall('/direct_messages/new.json',{user_id: '1234', 'text':'This is easy.'}, error, success);
```
To get the list of expected parameters and results, check [https://dev.twitter.com/rest/public](https://dev.twitter.com/rest/public)

## Included Functions

##### Search Tweets. [Documentation](https://dev.twitter.com/rest/reference/get/search/tweets)
To learn how to use Twitter Search effectively read [Using the Twitter Search API](https://dev.twitter.com/rest/public/search)
```javascript	
	twitter.getSearch(parameters, errorCallback, successCallback)
```


##### Update user's status (Tweet). [Documentation](https://dev.twitter.com/rest/reference/post/statuses/update)
```javascript
	twitter.postTweet(parameters, errorCallback, successCallback)
```
##### Follow a another user. [Documentation](https://dev.twitter.com/rest/reference/post/friendships/create)
```javascript
	twitter.postCreateFriendship(parameters, errorCallback, successCallback)
```
##### Get a user's timeline[Documentation](https://dev.twitter.com/rest/reference/get/statuses/user_timeline)
```javascript
	twitter.getUserTimeline(parameters, errorCallback, successCallback)
```
##### Get the latest 20 recent mentions for the authenticating user. [Documentation](https://dev.twitter.com/rest/reference/get/statuses/mentions_timeline)
```javascript
	twitter.getMentionsTimeline(parameters, errorCallback, successCallback)
```
##### Get the latest tweets and retweets by the authenticating users and the ones they follow. [Documentation](https://dev.twitter.com/rest/reference/get/statuses/home_timeline)
```javascript
	twitter.getHomeTimeline(parameters, errorCallback, successCallback)
```
##### Get latest retweets of authenticated user. [Documentation](https://dev.twitter.com/rest/reference/get/statuses/retweets_of_me)
```javascript
	twitter.getReTweetsOfMe(parameters, errorCallback, successCallback)
```
##### Get a tweet by id. [Documentation](https://dev.twitter.com/rest/reference/get/statuses/show/)
```javascript
	twitter.getTweet(parameters, errorCallback, successCallback)
```
##### Get information about a user by user\_id or handle (screen_name). [Documentation](https://dev.twitter.com/rest/reference/get/users/show)
```javascript
	twitter.getUser(parameters, errorCallback, successCallback)
```
##### Get a cursored collection of the followers of a user\_id or a handle (screen_name). [Documentation](https://dev.twitter.com/rest/reference/get/followers/list)
```javascript
	twitter.getFollowersList(parameters, errorCallback, successCallback)
```
##### Get a cursored collection of the followers' *ids* of a user\_id or a handle (screen_name). [Documentation](https://dev.twitter.com/rest/reference/get/followers/ids)
```javascript
	twitter.getFollowersIds(parameters, errorCallback, successCallbackok)
```
##### Upload media (images) to Twitter. [Documentation](https://dev.twitter.com/rest/reference/post/media/upload)
```javascript
	twitter.postMedia(parameters, errorCallback, successCallback)
```

## Tests

There is a test file `TwitterITSpec.js` that does a basic integration tests of the client. 
It uses a properties file `test/spec/properties.json` to inject in the OAuth properties. 
These will need to be updated with your own details before the tests will run

## Running tests

	make test