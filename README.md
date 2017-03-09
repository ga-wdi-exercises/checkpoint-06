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
.module ("blog",
["ui.router"]
)
```

### Question 2

One button below has an `ng-click` attribute; the other has `data-ng-click` instead. What difference does it make?

```html
<button ng-click="vm.create()">Click</button>
<button data-ng-click="vm.create()">Click</button>
```

```text
there is no difference interms of functionality but the only difference is that data-ng-click will pass through an html-validator while ng-click fails

[from angular docs on directives]
Directives have camel cased names such as ngBind. The directive can be invoked by translating the camel case name into snake case with these special characters :, -, or _.

Optionally the directive can be prefixed with x-, or data- to make it HTML validator compliant. Here is a list of some of the possible directive names: ng:bind, ng-bind, ng_bind, x-ng-bind and data-ng-bind.

```

### Question 3

Which of the three following options demonstrates the best usage of `ng-app`? **Explain your answer.**

```
all three can work without an error.
It kinda depends on the developer and the scope of the angular application that the developer wants to hava access to.
but you can't call data-ui-sref outside the scope.

#### A - demonstrates the better  use of ng-app directive for a developer that wants to have access of the directive as the element that ng-app is attached to will define the scope of the control of the angular application.This directive designates the root element of the application and should be placed to the root element of the html page which is near the root element of the page. e.g. <body> or <html>
      they all will work but in the B and C we still get the html element <h1>my App</h1> printed out but without a link
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
it's basically a link which helps change the view of your single page angular application depending on the state of your angular application without http request. no hard refresh,which makes it seamless for building great user interfaces and faster applications
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
class PostsController < ApplicationController
  def index
    @posts = Post.all

     respond_to do  |format|

       format.html { render html: @posts}
       format.json { render json: @posts}

     end
  end
end
```

### Question 7

Let's say the Posts in the previous question are available at `http://localhost:3000/posts`. In a front-end application, how could you do the following using AJAX?
  1. Retrieve all the posts in JSON form
  2. If Step 1 is successful, print the resulting JSON to the console
  3. If Step 1 is unsuccessful, print an error message to the console

```js
$.ajax({
  //on click use that IMDb value to look for a json data
  url: `http://localhost:3000/posts`,
  type: 'get',
  dataType: 'json',
}).done(response =>{
  console.log(response);
}).fail(() => {
  console.log("Ajax request fails!")

}).always(() => {
  console.log("This always happens regardless of successful ajax request or not.")
})
}
```

### Question 8

Using the same front-end application and Rails API from the previous question, how would you use AJAX to create a Post through the API? You can assume the following...
* The API is RESTful
* The `PostsController` contains a strong params method that is used when creating an instance of the `Post` model
* Each Post has `title` and `body` attributes, both of which are strings

If the Post creation is successful, the new Post should be printed to the browser console. Otherwise, an error message should be printed to the console.

```js


    $.ajax({
       type: 'POST',
       dataType: 'json',
       url: "http://localhost:3000",
       data: {
       post: {
           title: "How to look cool while wearing glasses",
           body: "I have always looked cool with glasses it's the best look there is."

        }
     }
    }).done((response) => {
      console.log(response);
    }).fail(() => {
      console.log("Failed to create.");
    })



```
