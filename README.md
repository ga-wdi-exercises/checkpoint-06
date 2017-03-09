## Instructions

1. Fork this repo
- Clone your fork
- Fill in your answers by writing the appropriate area or placing an 'x' in the square brackets for multiple-choice questions
- Add/Commit/Push your changes to Github
- Open a pull request

## Part I: Angular

### Question 1

Instantiate a new Angular module called `blog` that takes `ui.router` as a dependency.

```js
angular
  .module("blog", [ui.router])

```

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?

```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text
They are the same thing. You can use data-ng-click to make a valid html.
```

### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```text
#### A is the best usage of 'ng-app'
```

#### A

```html
<!DOCTYPE html>
<html data-ng-app="myapp">
  <head>
    <title>My app</title>
  </head>
  <body>
    <h1><a data-ui-sref="index">My App</a></h1>
    <div></div>
  </body>
</html>
```

#### B

```html
<!DOCTYPE html>
<html>
  <head data-ng-app="myapp">
    <title>My app</title>
  </head>
  <body>
    <h1><a data-ui-sref="index">My App</a></h1>
    <div></div>
  </body>
</html>
```

#### C

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My app</title>
  </head>
  <body>
    <h1><a data-ui-sref="index">My App</a></h1>
    <div data-ng-app="myapp"></div>
  </body>
</html>
```

### Question 4

Imagine an app in which a change to the view updates the model without a page refresh. Similarly, a change to the model updates the view without a page refresh.

Which one of the following concepts does this best illustrate?

```
[ ] A: Modularity
[ ] B: MVC
[XXXXX] C: Two-way data-binding
[ ] D: Separation of concerns
```

### Question 5

What is the `ui-sref` directive, and how is it used?

```text
A directive that binds a link (<a> tag) to a state. If the state has an associated URL, the directive will automatically generate & update the href attribute via the $state.href() method. Clicking the link will trigger a state transition with optional parameters. Also middle-clicking, right-clicking, and ctrl-clicking on the link will be handled natively by the browser.
```

## Part II: APIs & AJAX

### Question 6

Below is an `index` controller action that maps to a `Post` model in a Rails application. How would you modify it so that it can respond with a list of posts in either HTML or JSON form, depending on the incoming HTTP request?

```rb
class PostsController < ApplicationController
  def index
    @posts = Post.all
  end
end
```
```rb
 # app/views/index/test_ajax.html.erb

<div class="get">AJAX GET!</div>
<div class="post">AJAX POST!</div>
<div class="put">AJAX PUT!</div>
<div class="delete">AJAX DELETE!</div>
```

### Question 7

Let's say the Posts in the previous question are available at `http://localhost:3000/posts`. In a front-end application, how could you do the following using AJAX?
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js

  $.ajax({
  var url({http://localhost:3000/posts}
     url: url,
     type: "get",
     dataType: "json"
     <!-- // $.ajax takes an object as an argument with at least three key-value pairs...
     // (1) The URL endpoint for the JSON object.
     // (2) Type of HTTP request.
     // (3) Datatype. Usually JSON. -->
   }).done(() => {
     console.log("Ajax request success!")
   }).fail(() => {
     console.log("Ajax request fails!")
   }).always(() => {
     console.log("This always happens regardless of successful ajax request or not.")
   })
 })


```

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use AJAX to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js

.controller("PostShowController", [
   "PostController",
   "$stateParams",
   PostShowControllerFunction
 ]);

 function PostShowControllerFunction(PostController, $stateParams){
   this.post = postController.get({id: $stateParams.id});
 }

```
