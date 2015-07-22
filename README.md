Backbone.js App for JSON REST API
==============

This library provides a client-side interface for the [JSON REST API](https://github.com/WP-API/WP-API) plugin for WordPress. This code in this repository generates the Backbone JavaScript application that pairs with JSON REST API. Using this library, you can interact with WordPress installations that have JSON REST API installed using Backbone Models and Collections. Learn more about Backbone [here](http://backbonejs.org/).

## Usage

### Setup
The compiled JavaScript is included by JSON REST API by default. Compiled code is pulled into Github Pages which is enqueued by JSON REST API. That being said, this repository is setup as a WordPress plugin for development purposes. You can activate this plugin along side JSON REST API, and they will play nice together. The Client JS will dequeue the Github Pages version of the code and enqueue it's own. 

### Examples
The Backbone library supplies you with some Backbone models and collections for each route in the JSON REST API. A model
represents a single object such as a post. A collection represents a group of objects. We can use a model to pull a
specific post from a WordPress installation:

```javascript
var post = new wp.api.models.Post( { ID: 1 } );

post.fetch().done( function() {
    // post.attributes contain the attributes of the post
    console.log( post.attributes );
});
```

We can also grab a collection of posts:

```javascript
var posts = new wp.api.collections.Posts();

posts.fetch().done( function() {
    posts.each( function( post ) {
        // post.attributes contain the attributes of the post
        console.log( post.attributes );
    });
});
```

Requests are broken up into pages based on how posts_per_page is set or filtered. Therefore, sometimes we need to
paginate through a collection:

```javascript
var posts = new wp.api.collections.Posts();

posts.fetch().done( function() {
    posts.each( function( post ) {
        // post.attributes contain the attributes of the post
        console.log( post.attributes );
    });

    if ( posts.hasMore() ) {
        posts.more().done( function() {
            posts.each( function( post ) {
                // post.attributes contain the attributes of the post
                console.log( post.attributes );
            });
        });
    }
});
```
