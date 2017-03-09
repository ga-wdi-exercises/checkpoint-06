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
angular.module("blog", ["ui.router"])
```

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?



```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text
It does not make a difference, both will respond the same way.
```

### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```text
ng-app is a directive used to tell html to run angular and reference some javascript code. (A) is the best demonstration of ng-app because it is best to initialize it in the html tag.  
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
[x] C: Two-way data-binding
[ ] D: Separation of concerns
```

### Question 5

What is the `ui-sref` directive, and how is it used?

```text
ui-sref is equivalent to link_to in rails.  It establishes a link to the path or url that is referenced e.g. in the example above "<h1><a data-ui-sref="index">My App</a></h1>", "index" will be hyperlinked and when the user clicks on it, it will take them to 'My App' page
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

respond_to do |format|
 format.html { render :index }
 format.json { render json: @grumbles }
end
```

### Question 7

Let's say the Posts in the previous question are available at `http://localhost:3000/posts`. In a front-end application, how could you do the following using AJAX?
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js
$.ajax({
    url: url,
    type: "get",
    dataType: "json"
  }).done((response) => {
    console.log(response)
  }).fail(() => {
    console.log("Error, something went wrong!")
})

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use AJAX to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js
$.ajax({
  type: 'POST',
  data: {
    post: {
      title: "",
      body: "",
    }
  },
  dataType: 'json',
  url: "/posts"
}).done((response) =>  {
  console.log(response);
}).fail((response) => {
  console.log("AJAX POST failed");
})
```
