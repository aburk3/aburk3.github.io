---
layout: post
title:      "Rails Meets JavaScript"
date:       2019-04-23 09:53:25 +0000
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
	````



