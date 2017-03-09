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
  .module("blog", [
    "ui.router"
  ])

```

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?

```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text

The two are essentially identical except "data-ng-click" will pass an HTML validator and "ng-click" will not. Both work the same way, though.

```

### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```text

Option A is BY FAR the superior answer! Linking the entirety of the HTML to the application is in almost all circumstances infinitely better than linking only the "head" or one specific "div".

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
[X] C: Two-way data-binding
[ ] D: Separation of concerns
```

### Question 5

What is the `ui-sref` directive, and how is it used?

```text

"ui-sref" is used similarly to "href", but is the preferred choice when using angular. "ui-sref" will link to specific states within the router. Use it for links within your single-page application such that the state of the page changes, but you don't actually need to navigate to a new page.

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

put the following snippet between line 126 "@posts = Post.all" and line 127 "end"

  respond_to do |format|
    format.html { render :index }
    format.json { render json: @posts }
  end

```

### Question 7

Let's say the Posts in the previous question are available at `http://localhost:3000/posts`. In a front-end application, how could you do the following using AJAX?
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js

  $("button").on("click", () => {
    var url = "http://localhost:3000/posts"
    $.ajax({
      url: url,
      type: "get",
      dataType: "json"
    }).done((response) => {
      console.log(response);
    }).fail((response) => {
      console.log("Oh noes! Something went wrong!");
    })
  })


//I'm not sure my URL is correct. Does JSON need to be ion the URL somewhere?

```

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use AJAX to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js

//IN JS File

$(document).ready(() =>{
  $(".post").on("click", () => {

    let title = $(".title").val()
    let body = $(".body").val()

    $.ajax({
      type: "POST",
      data: {
        post: {
          title: title,
          body: body
        }
      },
      dataType: "json",
      url: "/posts"
    }).done((response) => {
      console.log(response);
    }).fail(() => {
      console.log("Oh noes! Something went wrong!");
    })
  })
})

//In Viewfile
  <label>Title:</label>
  <input class="title" type="text">
  <label>Content:</label>
  <input class="body" type="text">

```
