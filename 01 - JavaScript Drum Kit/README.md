# JavaScript Drum Kit
## App Logic
- When press different keys, the audios will be played
- While button is pressed, trasition occur first then disapear
- Everytime when the buttons is clicked, audio is replayed from start again(no delay between)

### const Declarations
`const` means "create constants". Since it is a constant, so we are not allowed to change the value the variable holds once it is set, at declaration time. A `const` declararion must have an explicit initialization even we want to set is as `undefined`. You'd have to declare `const a = undefined` to get it.

The scope of a `const` will be block scope, not funciton scope.

### Template Literals
If you have learned Ruby before, you may know "string interpolation"(#{..}). With string interpolation, we can embed a value into string.

```ruby
name = "Jon Snow"
puts "Hi, my name is #{name}"
#=> Hi, my name is Jon Snow
```

In ES6, we have a similar syntax call template literals(`${}`). We use ``..`` around a series of characters, which are interpreted as a string literal, but any expressions of the form ${..} are parsed and evaluated inline immediately.

```javascript
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
```

### play()
The `HTMLMediaElement.play()` method is used to play audio element.
```javascript
const audio = document.querySelector("audio")
audio.play()
```

### currentTime()
The `HTMLMediaElement.currentTime` property gives the current playback time in seconds. Setting this value seeks the media to the new time.

### transitionend
The `transitionend` event is fired when a CSS transition has completed. 

### data attribute

### transform attribute
The transform attribute defines a list of transform definitions that are applied to an element and the element's children.

We use scale here to enlarge out element.

```javascript
.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}
```

### transition
The transition CSS property is a shorthand property for transition-property, transition-duration, transition-timing-function, and transition-delay.

In our code we set all elements have animated property will transition, the `duration` is 0.07s and the `timing function` is `ease`.

```javascript
.key {
  transition: all .07s ease;
}

.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}
/ *
TransitionEvent {isTrusted: true, propertyName: "transform", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
TransitionEvent {isTrusted: true, propertyName: "border-right-color", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
TransitionEvent {isTrusted: true, propertyName: "border-bottom-color", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
TransitionEvent {isTrusted: true, propertyName: "border-top-color", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
TransitionEvent {isTrusted: true, propertyName: "border-left-color", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
TransitionEvent {isTrusted: true, propertyName: "box-shadow", elapsedTime: 0.07, pseudoElement: "", type: "transitionend", …}
* /
```

### TransitionEvent propertyName Property
```javascript
function playSound(e) {
  const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
  key.classList.add("playing");
}

function removeTransition(e) {
  if (e.propertyName !== 'transform') return;
  e.target.classList.remove('playing');
}
```
The TransitionEvent interface represents events providing information related to transitions(The CSS transition when animation occur).


The propertyName property returns the name of the CSS property associated with the transition, when a transitionevent occurs. The propertyName property is read-only.

In our example, there are several perperty are returned.

### data-* attributes
data-* attributes allow us to store extra information on standard. Any attribute on any element whose attribute name starts with data- is a data attribute.

In our example we use `data-key`
```html
<audio data-key="65" src="sounds/clap.wav"></audio>
```

We can use the `querySelector()` method to get the element which match a specified CSS selector in the document.
```javascript
key = document.querySelector(audio[data-key=65])
```

### event object
e.target
A reference to the object that dispatched the event

### Array.from
The Array.from() method creates a new Array instance from an array-like or iterable object.

We use this method to convert a nodeList to an array.
```javascript
const keys = Array.from(document.querySelectorAll('.key'));
```

While using `Element.querySelectorAll()`, it will return a non-live NodeList of all elements that matches the specified group of CSS selectors. The reason we want to convert the nodeList to array is because we want to use `forEach` method to to iterate through the collection.
**Note**
Although NodeList is not an Array, it is possible to iterate on it using forEach().  Several older browsers have not implemented this method yet.