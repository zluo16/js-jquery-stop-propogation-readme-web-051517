# Stop Propogation Readme

## Objectives

+ Explain what `stopPropogation()` is and why it's used
+ Explain "bubbling up"
+ Use stop propogation to prevent event handlers from bubbling up the DOM

## Intro


parent has click event and child has click event and you click child and therefore parent click event fires too, all events bubble up to window object
kill with stopPropogation

deepest node in doc will alert Document when fired but things higher up the chain won't fire lower

## Usage
HTML:
```html
<ul class="courses">
  <li class="course">
    Learn Ruby
      <span class='delete' data-id='1'>x</span>
    <div class="details">
      Learn Ruby, It loves you. Be happy.
    </div>
  </li>
</ul>
```

```

JS:
```js
$('.courses').on('click', '.course', function(){
    $(this).find('.details').slideToggle();
  });

  $('.course .delete').on('click', function(e){
    e.stopPropagation();
    alert("about to delete");
  })
```

when click `x`, will alert `"about to delete"` and then see course slide close because child event fires, and bubbles up so parent event fires. `stopPropogation` in child click event stops parent event from firing

examples of how to use `stopPropogation()`

## Instructions

+ some examples for students to practice with tests and in browser

## Resources
<p data-visibility='hidden'>View <a href='https://learn.co/lessons/js-jquery-stop-propogation-readme' title='Stop Propogation Readme'>Stop Propogation Readme</a> on Learn.co and start learning to code for free.</p>
