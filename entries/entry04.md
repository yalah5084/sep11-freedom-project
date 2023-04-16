# Entry 4
##### 04/16/23

### MVP

The teacher gave us the idea of using coordinates to find the lost pet for the MVP. However, we weren't sure how that would work with coordinates, then he showed us that the user can get the coordinates with [Google Maps](https://www.google.com/maps). The next step was to create the map. I had initially made a map in a separate file because our original plan was to have a separate home page and a separate map. Then, we changed our minds and wanted to do everything on one page so I had to move the map that I already made to the main page. I encountered a small problem which was making the map smaller. I searched on Google how to make a Leaflet map smaller and I didn't find anything. Until I remembered that the first thing I did when I learned Leaflet was to set the map to the size of the screen with CSS. I originally had:

```cs
#map {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}
```

I started by changing the position to relative, but the map disappeared. After tinkering with the values of the sides and adding h1s, I figured that the problem was that I didn't set a width and a height. I set the width to `1300px` and the height to `600px`. I also realized that I didn't need position: relative and I only needed margin: auto to center the map horizontally.

![image](https://user-images.githubusercontent.com/91745172/232341985-1cafe1dc-434d-4270-8d8f-83c06a6c41bf.png)

My partner Hanna had already written the HTML so that the user could provide the coordinates and the pet's name. So my next step was to use the provided coordinates and make a marker on the map. I gave an event listener to the button and put `L.marker([userLong, userLat]).addTo(map)` inside the button so that it creates a marker once the button was clicked. However, it didn't work. Then, I thought of using a function. I created a function called `petMarker` with two parameters and I call the function when the button is clicked:

```js
button.addEventListener("click", function() {
  petMarker(userLong.value, userLat.value) // use the coordinates to add a marker to the map
})

function petMarker(long, lat) {
    L.marker([long, lat]).addTo(map) // add marker to the map
}
```

Another thing I wanted to do was to add popups with the pet's name so I added a `bindPopup()` function to the marker. I also added `{closeOnClick: false, autoClose: false}` because I didn't want the popup to close when the user clicks somewhere else on the page. 

```js
function petMarker(long, lat) {
    L.marker([long, lat]).addTo(map).bindPopup(petName.value, {closeOnClick: false, autoClose: false}).addTo(map) // add marker and popup to the map
}
```

I wanted the popup to open once it was created, so I tried to add `.openPopup()` before `.addTo(map)`. But the popup didn't open at first. I didn't understand what the problem was, so I went back to the file where I tinkered with my tool and noticed that the marker was stored in a variable and the order of `.addTo(map)`, `.bindPopup()` and `.openPopup()` was different. I had to add the marker to the map first, then make a popup, and then open it. 

```js
 function petMarker(long, lat) {
    var marker = L.marker([long, lat]).addTo(map) // add marker to the map
    marker.bindPopup(petName.value, {closeOnClick: false, autoClose: false}).openPopup() // add pet name to the marker and make sure it's open
}
```

![image](https://user-images.githubusercontent.com/91745172/232342048-d72ac545-0afa-477a-9d8f-9dad49e48ccd.png)



[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
