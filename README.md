# Week 08

## Instructions

1. Fork this repo
- Clone your fork
- Fill in your answers by writing the appropriate area, or placing an 'x' in the square brackets for multiple-choice questions
- Add/Commit/Push your changes to Github
- Open a pull request

## Part I: Angular

### Question 1

Instantiate a new Angular module called `blog` that takes `ui.router` as a dependency.

```js
angular
  .module("blog", ["ui.router"])
  .config(["$stateProvider", Router])

function Router($stateProvider) {
}
```

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?

```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text
they perform the same function but the only difference is that data-ng-click can pass data as an argument(?) and it can pass HTML validators.
```

### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```text
Option A is the best answer because it allows ng-app to be applied throughout the entire web application since it is located within the html tag. Option b will only applied ng-app in the head and Option C will give you an error because it is beneath another angular function(?).
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

Imagine an app in which a change to the view updates the model without a page refresh, and a change to the model updates the view without a page refresh.

Which one of the following concepts does this best illustrate?

```
[ ] A: Modularity
[ ] B: MVC
[*] C: Two-way data-binding
[ ] D: Separation of concerns
```

### Question 5

What is the `ui-sref` directive, and how is it used?

```text
It's basically a link to another page, kind of like href except instead of providing a URL or a directory path you simply refer to the name of the state that is associated with the url that you want to direct to.
```

## Part II: APIs

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
class PostsController < ApplicationController
  respond_to: :html, :json

  def index
    @posts = Post.all
    respond_with(@posts)
  end
end
```

### Question 7

Let's say the Posts in the previous question are available when you visit `http://localhost:3000`. In a front-end application, how could you do the following using jQuery...
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js
$.ajax({
  url: "http://localhost:3000",
  type: 'get',
  dataType: 'json'
}).done((result) => {
  console.log(result);
}).fail(() => {
  console.log("YOU HAVE FAILED AT UNDERSTANDING AJAX AND JSON!");
})
```

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use jQuery to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js
$.ajax({
  url: "http://localhost:3000",
  type: 'post',
  dataType: 'json',
  data: {
    post: {
      title: "AJAX and API",
      body: "JSON"
    }
  },
}).done((post) => {
  console.log(post);
}).fail(() => {
  console.log("YOU HAVE FAILED AT UNDERSTANDING AJAX AND JSON!");
)
})
```
