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

### Click handlers

Consider this view:

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

A click handler is specified by an `events` object. The property name specifies the elements where an handler should be attached. The value is the method name which will be called on click.

Html: 

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

