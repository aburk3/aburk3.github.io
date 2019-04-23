---
layout: post
title:      "Rails Meets JavaScript"
date:       2019-04-23 05:53:25 -0400
permalink:  rails_meets_javascript
---


I've recently finished my Rails and JavaScript project and it's been quite fun.  I love integrating the different pieces of an application and watching them all come together. Learning how to use JavaScript/jQuery to interact with the Rails back-end has been awesome. 

For my project I essentially built a very simple web-application that allows a `User` to create an account with password encryption, create a `Post`, and add associated `Comment`s to that post. I utilized the ActiveModel:Serializer to create the Post and Comment model files thereby serializing the Ruby objects to JSON.

```
class PostSerializer < ActiveModel::Serializer
  attributes :id, :title, :content, :user
  has_many :comments
  belongs_to :user
end

......

class CommentSerializer < ActiveModel::Serializer
  attributes :id, :content, :user, :post
  belongs_to :post
end
```

In order to render the HTML I wanted with JavaScript I decided to simply wrap the content being yielded in my `application/layout` in a `div` that had an id of `id="app-container"`. The reason for this was so that I could simply clear the content of the `div` and append new content via JavaScript or jQuery selector whenver new data was received. 

In order to render a Post show page my JavaScript looks like:

```
$(document).on('click', ".show_link", function(e) {
    e.preventDefault()
    $('#app-container').html('')
    let id = $(this).attr('data-id')
    fetch(`/posts/${id}.json`)
    .then(res => res.json())
    .then(post => {
      let newPost = new Post(post)

      let postHtml = newPost.formatShow()

      $('#app-container').append(postHtml)
    })
  })
	```
	
	The core of this bit of code can be explained as follows:
	1. Upon clicking the link for a Post, Prevent the default action of refreshing the page (`e.preventDefault()`)
	2. Clear the designated container of all HTML in prepartion for new data (`$('#app-container').html('')`)
	3. `Fetch` the Post object of the link you clicked by using the `data-id` attribute assigned to the link and using it in the route (`fetch('/posts/${id}.json'`)
	4. Receive a JSON as the response object and use it to create a JavaScript Post Object (`new Post(post)`) by passing the post to the constructor function
	5. Format the HTML for the Post's show page by calling on a function for creating custom HTML (`newPost.formatShow()`)
	6. Finally, append the formatted Post to the container that you cleared out earlier!

This is a small example of how a simple container can be used by JavaScript to allow for dynamic content to be displayed without a prevent page refresh. 

Although this is an example of fetching data, the functions that allow for POSTing data don't look all that different:

```
 $('#new_post').on('submit', function(e) {
    e.preventDefault();
    const values = $(this).serialize();

    /**
     * Makes AJAX post,
     * clears container html,
     * creates Post object, formats HTML,
     * and appends HTML to container
     */
    $.post('/posts', values).done(function(data) {
      $('#app-container').html('');
      const newPost = new Post(data)
      const htmlToAdd = newPost.formatShow()

      $('#app-container').html(htmlToAdd);
    })
  })
}
```

It took me a little while to get used to using JavaScript with Rails, but once I started to see the patterns it all became a whole lot easier!


