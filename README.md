# JS Cheat sheet
This is my personal JavaScript cheat sheet

## jQuery
### Get clicked item in event handler

Get the current clicked item in click handler
```JavaScript
    function clicked(e){
      e.preventDefault();
      var id = $(e.currentTarget);
    }
```

## backbone.js
### Create a new model

Argument to `extend` stays empty.

```JavaScript
    var PodcastFeed = Backbone.Model.extend({ });
```

Create a new feed:

```JavaScript
    var cre = new PodcastFeed(
    { 
      id: "1",
      title: "CRE", 
      image: "http://meta.metaebene.me/media/cre/cre-logo-1400x1400.jpg"
    });
```

`PodcastFeed` gets an object with feed properties.

### Access an model property
```JavaScript
    var title = cre.get("title");
```

### Set model property after instantiation

```JavaScript
    var person = new Person();
    person.set({ name: "Thomas", age: 67});
```

### Click handlers

Consider this view:
```JavaScript
    var PodcastView = Backbone.View.extend({
      tagName: "ul",

      events: {
        'click .podcast-list-item img' : 'thumbnailClicked'
      },

      thumbnailClicked: function(e){
        e.preventDefault();
        var id = $(e.currentTarget).data("id");
        var item = this.collection.get(id);
        alert(item.get("title"));
      },

      render: function(){
          var template = $("#item-template");
          var el = $(this.el);
          this.collection.each(function(model){
              var html = template.tmpl(model.toJSON());
              el.append(html);
          });
      }
    });
```
A click handler is specified by an `events` object. The property name specifies the elements where an handler should be attached. The value is the method name which will be called on click.

Html: 
```HTML
    <!-- Template for a single item -->
    <script id="item-template" type="text/x-jquery-tmpl">
      <li class="span2">
         <div class="podcast-list-item">
           <a href="#" class="thumbnail">
            <img data-id="${id}" data-src="${image}" alt="${title}" src="${image}">
           </a>
         </div>
      </li>
    </script>

    <!-- The view will be shown here -->
    <div id="feed-list" class="span2">
      
    </div>
```
### Add class name to view
There will be the case you want to add a class to your view being rendered. Simply add a `className` property to your view:

```JavaScript
    var FooView = Backbone.View.extend({
       tagName: "ul",
       className: "unstyled", //the class unstyled will be added on render automatically
       render: function(){
        //render your view here
       }
    });
```

### Base a view on an existing element

```HTML
  <div id="foo">
  </div>
```

```JavaScript
  var MyView = Backbone.View.extend({
    el: "#foo",
    render: function(){
      $(this.el).empty(); //Empties the view before actual rendering. 
    }
  });
  var view = new MyView();
  view.render();  //No need to insert the rendered html manually into #foo. Backbone handles that automatically in this case.
```

### Load data from service

```JavaScript
    var MyModel = Backbone.Model.extend();
    var MyCollection = Backbone.Collection.extend({
        url: '/getData',
        model: MyModel
    });
```
At first create a new model and collection. The collection needs an `url` where it can fetch data from.

Load data:
```JavaScript
    var foo = new MyCollection();
    foo.fetch({
        success: function(){ /*Yay, new data*/ },
        error: function() { /*Sorry dude, you screw up*/ }
    });
```

`fetch` does the actual service call and fills the models.

### Render view after data was loaded
Source: [StackOverflow](http://stackoverflow.com/a/11290928/2381304)

We want to render our models *after* they were loaded from service.
```JavaScript
    var MyView = Backbone.View.extend({
        initialize: function(){
            var self = this;
            this.collection.fetch().complete(function(){
                self.render();
            });
        },
        render: function(){
            this.collection.each(function(element){
                //render your model here
            });
        }
    });
    var view = new MyView({
        collection: myCollection
    });
```

### Tutorials
- http://backbonetutorials.com/what-is-a-model/

## node.js

### Tutorials
- http://blog.modulus.io/absolute-beginners-guide-to-nodejs
