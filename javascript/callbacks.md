Callbacks, how do they work?  First I wanted to ask Eduardo just the syntax and
copy and paste it in.  Then he went into a long discussion about what objects
are.

You can assign anything to a variable, even a function.
```
var foo = 1;
var foo = 1.0;
var foo = 'i am a string';
var foo = [1, 2, 3];
var foo = {};
var foo = function() {
  console.log('hi i'm a function');
}
```

Now I can go foo(), and it calls the anonymous function assigned to my variable.
This is syntatic sugar created to make javascript more like C or C++.  I don't
really remember which.  In actuality, it should be doing foo.apply();

Anyways, the point is that functions are also data types.  You can assign them
to variables.  You can pass them in as arguments to another function.  You can
even assign them to a key in an object literal.

```
var sayHello = function() {
  console.log(this);
};

var myDanceJournal = {
  entries: 3,
  pages: 100,
  speak: sayHello
}
```

What is `this` when `sayHello()` is called versus when `myDanceJournal.speak()`
is called?  In the first case, there is no dot- notation of calling the method.
So the `window` object is what is implied.  In `myDanceJournal.speak()`, `this`
is `myDanceJournal`.  So the point here is that `this` can be tricky when you
pass functions around.  It's not always what you think it is.

```
$.ajax({
  url: someURL,
  data: data,
  dataType: 'json',
  complete: function(response) {
    alert('it has completed');
  }
});
```

What is actually happening up there?  `$.ajax` is a function, and we're passing
it an object literal as an argument, kind of like a hash.  The complete key
points to an anonymous function.  On completion of the ajax call, `$.ajax` will
call the function that is stored in `complete`.
