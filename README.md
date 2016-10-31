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

<app.js>
// Your answer goes here...
.module("blog", [
  "ui.router"
])

``<index.html File>`

<!DOCTYPE html>
<html data-ng-app="blog">
  <head>
    <title>Blog</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/0.2.15/angular-ui-router.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.0-beta.2/angular-resource.min.js"></script>

    <script src="js/app.js"></script>
  </head>
  <body>
    <h1>Blog</h1>
    <main data-ui-view></main>
  </body>
</html>

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?

```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text
They both are the same thing. The only difference is that the HTML 5 Validator will pass the data-ng-click element.

```
### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```text
Best Usage is a relative term, depending on where you put it will limit the scope. therefore when it is in the html tag, it defines the entire page scope. where as a single DIV is may be faster because it is limited in scope.  In our use of a SPA, we tend to place it in the HTML or Body tag, so Reference A would seem to be the best.

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
[X] C: Two-way data-binding
[ ] D: Separation of concerns
```

### Question 5

What is the `ui-sref` directive, and how is it used?

```text
ui-sref is used in <a>...</a> and  used to transfer control to a new state.
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
def index
    @posts = Post.all
    respond_to do |format|
      format.html { render :index }
      format.json { render json: @grumbles }
    end
  end
```

### Question 7

Let's say the Posts in the previous question are available when you visit `http://localhost:3000`. In a front-end application, how could you do the following using jQuery...
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js
def index
  @posts= Post.all

  respond_to do |format|
    if @grumble.save!
      format.html { redirect_to @grumble, notice: 'Grumble was successfully created.' }
      format.json { render json: @grumble, status: :created, location: @grumble }
    else
      format.html { render :new }
      format.json { render json: @post.errors, status: :unprocessable_entity }
    end
  end
end
```

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use jQuery to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js
$(".get").on("click", () => {
  $.ajax({
    type: 'POST',
    dataType: 'json',
    url: "/posts"
  }).done((response) =>  {
    console.log(response);
  }).fail((response) => {
    console.log("Ajax get request failed.");
  })
})
```
