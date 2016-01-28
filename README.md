# Stop Propagation Readme

## Objectives

+ Explain what `stopPropagation()` is and why it's used
+ Explain "bubbling up"
+ Use stop propagation to prevent event handlers from bubbling up the DOM

## Intro

Let's say you're building a course registration site for a Flatiron. You need to build a list of available course, and include some details about each course.

You need to build is so that when you click a course, the details about the course disappear and reappear. Each course would need to have a click event that toggles the details. Flatiron also wants to be able to remove courses if they're not offered that semester, so there will need to be a button that removes that course (an `x`)

We'd end up with some HTML like this:

```html
<ul class="courses">
  <li class="course">
    Ruby
      <span class='delete'>x</span>
    <div class="detail">
      Learn Ruby, It loves you. Be happy.
    </div>
  </li>
  <li class="course">
    JavaScript
      <span class='delete'>x</span>
    <div class="detail">
      Learn JavaScript and build powerful full stack web apps
    </div>
  </li>
  <li class="course">
    iOS
      <span class='delete'>x</span>
    <div class="detail">
      Everyone loves a good iPhone app
    </div>
  </li>
</ul>
```

And let's say we create those click events:

```js
$('.course').on('click', function(){
    $(this).find('.details').slideToggle();
  });

  $('.course .delete').on('click', function(){
    alert("about to delete");
  })
```

The first click event toggles the details on and off the screen. The second click event just alerts `"about to delete"`.

Open `index.html` in the browser and `js/script.js` in the text editor. Make sure all the code in `js/script.js` is commented out expect the code under the comment `// toggle and delete`.

Go ahead and first click `Ruby` in the browser to hide the details. Then click the `x` to "delete" the item. You should see the alert appear, as we expected. But wait, why do the details toggle on the screen? How did that event happen?

## Bubbling Up

In jQuery, all click events "bubble up" the DOM. The `document` object knows about every event that is triggered on a page. This means that in our example above, the `span` with the `x` is a child of the `li` with the class `course`. When we click the `x`, that click event bubbles up the DOM and the parent element, the `li` knows a click event has been triggered, and that triggers the click event of the parent. 

What in the world? Why is that behavior we would want? In most cases you wouldn't at all. Imagine if you had a large series of nested elements all with click events. Firing the click event of the innermost child would trigger the click events of every single parent.

## Stop Propagation

So how the heck do we stop that from happening? With `stopPropagation`. Let's go ahead and refactor our jQuery:

```js
$('.course').on('click', function(){
    $(this).find('.details').slideToggle();
  });

  $('.course .delete').on('click', function(event){
    alert("about to delete");
    event.stoppropagation();
  })
```

You'll notice we didn't change anything to the click event on the class `course`. But we did make some changes to the delete button. We passed `event` to the anonymous function and then called the `stoppropagation` function on the event object. This function stops the click event from bubbling up the dom.

Go ahead and comment out all the code in `js/script.js` except the code under the comment `//stop propagation`. Refresh the page in the browser. Click a course name to hide the details and then click the `x`. The alert should appear and the details should remain hidden.

## Resources

+ [jQuery Docs](https://api.jquery.com/event.stoppropagation/)
+ [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)