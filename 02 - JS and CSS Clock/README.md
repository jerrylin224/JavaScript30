# JS and CSS Clock
## App Logic
- Let the each hands rotate based on the current time

### Initialize the hands and rotate
- transform-origin: 100%;
- transform: rotate(90deg);

#### transform-origin
The transform-origin property lets you modify the origin for transformations of an element. The nitial value is 50% 50%, which means if you rotate an element, the transformation origin will be the center of the element.
```css
.hand {
  transform-origin: 100%;
}
```
In our example, we have to set the `transform-origin` as 100% to make the transform origin become the far right of the element(hand), which coincidently is the center of the clock.

#### transform: rotate(n deg)
The rotate() CSS function defines a transformation that moves the element around a fixed point (as specified by the transform-origin property) without deforming it.

In our example, we have to rotate the hand for 90 degree to turn it from horizontal to vertical. Then the hand can start from the right place.
```css
.hand {
  transform: rotate(90deg);
}
```
### Get current time
#### getSeconds(), getMinutes() and getHours()
In this project we use the three methods to the current second, minute and hour. We first instantiate a now object by invoking `new Date()`. The we use the method to get current time.

```javascript
const now = new Date();
const secondHand = document.querySelector('.second-hand');
const seconds = now.getSeconds();
const mins = now.getMinutes();
const hours = now.getHours();
const secondDegrees = ((seconds / 60) * 360) + 90;

secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
```
### Set interval
We want all the hands move at every second, just like a real clock. So we use `setInterval` to trigger the function every second.

Also don't forget to invoke the method first, or there will be a leap while user open the page(first all three hands are at the orignal places, then jump to new places).
```javascript
function setDate() {
  // ...
}

setInterval(setDate, 1000);

setDate();
```
