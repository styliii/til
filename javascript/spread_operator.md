## Spread Operators

I generally stay away from the javascript in our code base, but avoiding is no
longer optional.  I've been noticing a lot of `...` all over, which
instinctively makes me think of ranges.  In javascript, 3 dots are called the
*spread operator*.  It's used all over the place because one of the tenants of
redux is do not mutate the state object for better reliability of outcome.

The spread operator allows you to create a new object, while copying attributes from
the old one, sidestepping the need to mutate the original object.

#### Usage
```javascript
const myArray = [1, 2, 3];
const newArray = [...myArray, 4];
console.log(newArray);
  [1, 2, 3, 4]

const myObject = { checked: true, name: 'li' };
const newObject = { ...myObject, name: 'chhay' };
console.log(newObject);
  Object {checked: true, name: 'chhay'}
```
