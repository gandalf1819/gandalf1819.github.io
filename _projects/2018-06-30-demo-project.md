---
title: 'Webber'
subtitle: 'A simple web application, comprised of a web server written in Go'
date: 2018-06-30 00:00:00
featured_image: '/images/go.png'
---

![](/images/go.png)

## Webber

Webber is a simple web application, comprised of a web server written in Go.


### Features

Webber provides the following features in the application.

* User registration with username and password.
* Logging in as a given user, given username and password.
* Users can follow or unfollow other users.
* Users can create posts that are associated with their profile.
* Users can view posts of the users who they follow on their news feed.

### Project Schema

	|-- handler
		|-- auth.go --> authentication module, allows user registration and login portal.
		|-- init.go --> initialization module, initializes the connectors module.
		|-- post.go --> config for post module, implementation of post, follow and unfollow functionality.
		|-- response.go --> returns API response to user.
		|-- connectors.go --> connectors module, handles connections to authentication, user and userpost services.
	|-- services
		|-- auth
			|-- auth_driver --> handles token initialization, generation and deletion.
				|-- driver.go
			|-- auth_server --> authentication server module.
				|-- server.go
			|-- auth_test --> authetication testing module, contains test cases for the functions of driver.go.
				|-- client.go
				|-- auth_test.go
				|-- runTestCases.sh --> shell script to start test client and run test cases
			|-- authpb --> gRPC function calls using protocol buffers.
				|-- auth.pb.go
				|-- auth.proto
			|-- runAuthService.sh --> shell script to run Auth Service   
		|-- post
			|-- post_driver --> add new posts and retrieve follower posts functionalities. 
				|-- driver.go
			|-- post_server --> post server module.
				|-- server.go
			|-- test --> post testing module, contains test cases for the functions of driver.go.
				|-- client.go
				|-- post_test.go
				|-- runTestCases.sh --> shell script to start test client and run test cases	
			|-- postpb --> gRPC function calls using protocol buffers.
				|-- post.pb.go
				|-- post.proto
			|-- runPostService.sh --> shell script to run Post Service   
		|-- user
			|-- user_driver --> implementation of user module functionalities.
				|-- driver.go
			|-- user_server --> user server module.
				|-- server.go
			|-- test --> user testing module, contains test cases for the user module functionalities of user.go.
				|-- client.go
				|-- user_test.go
				|-- runTestCases.sh --> shell script to start test client and run test cases
			|-- userpb --> gRPC function calls using protocol buffers.
				|-- user.pb.go
				|-- user.proto
			|-- runUserService.sh --> shell script to run User Service
	|-- raft
		|-- raftexample-1
		|-- raftexample-2
		|-- raftexample-3
		|-- app.exe
		|-- listener.go
		|-- main.go
		|-- raft.go
		|-- raftexample_test.go
	|--views
		|--css
			|-- main.css --> stylesheet for mini-twitter
			|-- toastr.css --> stylesheet for toastr functionality
		|--html
			|-- login.html --> homepage containing user login and user registration features
			|-- posts.html --> posts page containing friends, newsfeed and posts features
		|--images
		|--js
			|-- api.js --> function definitions for user registration, signIn, followUser, unfollowUser, addPost, logout
			|-- login.js --> function definition for toggleTab for loginForm, registerForm
			|-- posts.js --> function definition for toggleTab for friends, newsfeed and status tabs
			|-- toastr.js --> function definitions for toastr features
	|--web
		|--server.go --> build target (the code that actually runs the server)
	|-- runBackendServer.sh --> port specifications and command to start the server

### RAFT Implementation

Raft is a distributed consensus algorithm. It solves the problem of getting multiple servers to agree on a shared state even in the face of failures. The shared status is usually a data structure supported by a replicated log. We need the system to be fully operational as long as a majority of the servers are up.

Raft works by electing a leader in the cluster. The leader is responsible for accepting client requests and managing the replication of the log to other servers. The data flows only in one direction: from leader to other servers.

Raft decomposes consensus into three sub-problems:

* Leader Election: A new leader needs to be elected in case of the failure of an existing one.

* Log replication: The leader needs to keep the logs of all servers in sync with its own through replication.

* Safety: If one of the servers has committed a log entry at a particular index, no other server can apply a different log entry for that index.

### Running the application

Go to the Webber folder and in the terminal run the following command:

./runBackendServer.sh

The PORT property can be changed in the runBackendServer.sh file.

Open you web browser and go to the following address:

https://localhost:9090/login

Use the same port that is defined in the runBackendServer.sh file.

Launch the post, user and auth services with the help of shell scripts file defined in the respective services folder.

To start the raft cluster, go to raft folder and run goreman start.

Check the code for the application here: [Webber](https://github.com/gandalf1819/Webber)

<!-- ## Demo content

This page is a demo that shows everything you can do inside portfolio and blog posts.

We've included everything you need to create engaging posts about your work, and show off your case studies in a beautiful way.

**Obviously,** we’ve styled up *all the basic* text formatting options [available in markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

You can create lists:

* Simple bulleted lists
* Like this one
* Are cool

And:

1. Numbered lists
2. Like this other one
3. Are great too

You can also add blockquotes, which are shown at a larger width to help break up the layout and draw attention to key parts of your content:

> “Simple can be harder than complex: You have to work hard to get your thinking clean to make it simple. But it’s worth it in the end because once you get there, you can move mountains.”

The theme also supports markdown tables:

| Item                 | Author        | Supports tables? | Price |
|----------------------|---------------|------------------|-------|
| Duet Jekyll Theme    | Jekyll Themes | Yes              | $39   |
| Index Jekyll Theme   | Jekyll Themes | Yes              | $39   |
| Journal Jekyll Theme | Jekyll Themes | Yes              | $39   |

You can throw in some horizontal rules too:

---

### Image galleries

Here's a really neat custom feature we added – galleries:

<div class="gallery" data-columns="3">
	<img src="/images/demo/demo-portrait.jpg">
	<img src="/images/demo/demo-landscape.jpg">
	<img src="/images/demo/demo-square.jpg">
	<img src="/images/demo/demo-landscape-2.jpg">
</div>

Inspired by the Galleries feature from WordPress, we've made it easy to create grid layouts for your images. Just use a bit of simple HTML in your post to create a masonry grid image layout:

```html
<div class="gallery" data-columns="3">
    <img src="/images/demo/demo-portrait.jpg">
    <img src="/images/demo/demo-landscape.jpg">
    <img src="/images/demo/demo-square.jpg">
    <img src="/images/demo/demo-landscape-2.jpg">
</div>
```

*See what we did there? Code and syntax highlighting is built-in too!*

Change the number inside the 'columns' setting to create different types of gallery for all kinds of purposes. You can even click on each image to seamlessly enlarge it on the page.

---

### Image carousels

Here's another gallery with only one column, which creates a carousel slide-show instead.

A nice little feature: the carousel only advances when it is in view, so your visitors won't scroll down to find it half way through your images.

<div class="gallery" data-columns="1">
	<img src="/images/demo/demo-landscape.jpg">
	<img src="/images/demo/demo-landscape-2.jpg">
</div>

### What about videos?

Videos are an awesome way to show off your work in a more engaging and personal way, and we’ve made sure they work great on our themes. Just paste an embed code from YouTube or Vimeo, and the theme makes sure it displays perfectly:

<iframe src="https://player.vimeo.com/video/19536258?color=ffffff&title=0&byline=0&portrait=0" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

---

## Pretty cool, huh?

We've packed this theme with powerful features to show off your work. Why not put them to use on your new portfolio?

<a href="https://jekyllthemes.io/theme/index-portfolio-jekyll-theme" class="button button--large">Get This Theme</a> -->