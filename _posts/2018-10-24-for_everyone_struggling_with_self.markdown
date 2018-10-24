---
layout: post
title:      "For Everyone Struggling with `Self`"
date:       2018-10-24 15:30:54 -0400
permalink:  for_everyone_struggling_with_self
---


I struggled with the concept of `self` in Ruby for a little longer than necessary I believe. So, I wanted to add to the 

literature out there so that any newcomer may not get held up on it for as long as I did. 
<br>
<br>
<br>
*In short*  - and skipping all the nuances - `self` refers to that which it is called on. 

What does that mean though?
<br>
<br>
```
def run_through_snow
  self
end
```
<br>
<br>
Okay what is `self` referring to here? The answer I kept running into was, "It is refferring to whatever object the 

method is called on." But this didn't make things clear for me. Let's put it into context.
<br>
<br>
<br>
Imagine you have an instance of a Dog (class) set to a variable "Skimpy."

`Skimpy = Dog.new("Skimpy")  ## this name is being set as an instance variable @name` 
<br>
<br>
Next, let's say that we want to call the `run_through_snow` method from earlier on the variable `Skimpy`?

`self` is equal to `#<Dog:000000000000 @name="Skimpy">`
<br>
<br>
My mind had trouble grasping this until I used `binding.pry` and actually checked the value of `self` and saw things for myself. 

If you set a binding.pry in the method, such as:
<br>
<br>
```
def run_through_snow
  self
  binding.pry
end
```
<br>
<br>
When you drop into pry you can see for yourself.

`self` will return the instance of the Dog class we created earlier.


`#<Dog:000000000000 @name="Skimpy">`


`self.name` will return what? 
<br>
**Exactly**
<br>
`self.name` will return "Skimpy"









