# JS Cheat sheet
This is my personal JavaScript cheat sheet

## jQuery
### Get clicked item in event handler

Get the current clicked item in click handler
    function clicked(e){
      e.preventDefault();
      var id = $(e.currentTarget);
    }

## backbone.js
### Create a new model

Argument to `extend` stays empty.

    var PodcastFeed = Backbone.Model.extend({ });

Create a new feed:

    var cre = new PodcastFeed(
    { 
      id: "1",
      title: "CRE", 
      image: "http://meta.metaebene.me/media/cre/cre-logo-1400x1400.jpg"
    });

`PodcastFeed` gets an object with feed properties.

### Access an model property

    var title = cre.get("title");