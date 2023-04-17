# Entry 4
##### 04/16/23

### Tinker with tool

I wanted to know how to remove a marker so I googled "how to remove markers on Leaflet js." My first result was [Stack Overflow](https://stackoverflow.com/questions/9912145/leaflet-how-to-find-existing-markers-and-delete-markers#:~:text=removeLayer()%20and%20it%20gets,Hope%20that%20helps%20you%20out!&text=Save%20this%20answer.,-Show%20activity%20on), but as I scrolled, I didn't understand anything. I decided to go on Youtube and found a helpful [tutorial](https://www.youtube.com/watch?v=tJWE7Fe_i-k&ab_channel=AnartzMugikaLedo-Desarrollo%26Formaci%C3%B3n) in Spanish. After watching the video, I changed a few things and only used what I needed. Instead of `move`, I wanted to use double click, but I forgot how it was written so I looked up the [Leaflet reference](https://leafletjs.com/reference.html#map-dblclick). I didn't need `draggable: true`, but it gave me a good idea for my freedom project to let the user drag the marker. `removeLayer()` is what removes the marker. I ended up with this:

```js
var leafMarker = L.marker([51.5,-0.09], {icon: leafIcon).addTo(map) // make leaf marker
leafMarker.on('dblclick', () => map.removeLayer(leafMarker)) // double click to delete marker
```

In the same leaflet reference, I found the [`on()` method](https://leafletjs.com/reference.html#evented-on) that the guy was using and since I didn't understand what `() =>` was, I was hoping that it would clarify my question. However, I saw the different syntaxes for the method and realized that I could use `function(){}` instead of `() =>`. I was curious to see if I could use `addEventListener()` instead of `on()` so I tried it and I actually can.

```js
leafMarker.on('dblclick', function() {map.removeLayer(leafMarker)})
// OR
leafMarker.addEventListener('dblclick', function() {map.removeLayer(leafMarker)})
```

Before double clicking:

![image](https://user-images.githubusercontent.com/91745172/232350517-c9189e1c-5ed8-4da4-8863-1d9024cacff8.png)

After double clicking:

![image](https://user-images.githubusercontent.com/91745172/232350703-fe882a12-e628-4583-9d8f-e0c0003248b0.png)

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

Another thing I wanted to do was to add popups with the pet's name so I added a `bindPopup()` to the marker. I also added `{closeOnClick: false, autoClose: false}` because I didn't want the popup to close when the user clicks somewhere else on the page. 

```js
function petMarker(long, lat) {
    L.marker([long, lat]).addTo(map).bindPopup(petName.value, {closeOnClick: false, autoClose: false}).addTo(map) // add marker and popup to the map
}
```

I wanted the popup to open once it was created, so I tried to add `openPopup()` before `addTo(map)`. But the popup didn't open at first. I didn't understand what the problem was, so I went back to the file where I tinkered with my tool and noticed that the marker was stored in a variable and the order of `addTo(map)`, `bindPopup()` and `openPopup()` was different. I had to add the marker to the map first, then make a popup, and then open it. 

```js
 function petMarker(long, lat) {
    var marker = L.marker([long, lat]).addTo(map) // add marker to the map
    marker.bindPopup(petName.value, {closeOnClick: false, autoClose: false}).openPopup() // add pet name to the marker and make sure it's open
}
```

![image](https://user-images.githubusercontent.com/91745172/232342048-d72ac545-0afa-477a-9d8f-9dad49e48ccd.png)

Lastly, I wanted the user to be able to remove the markers and evn drag them. After the last time I tinkered with my tool, I found a way to remove and drag the marker. I remember seeing {draggable: true} on the [Stack Overflow](https://stackoverflow.com/questions/9912145/leaflet-how-to-find-existing-markers-and-delete-markers#:~:text=removeLayer()%20and%20it%20gets,Hope%20that%20helps%20you%20out!&text=Save%20this%20answer.,-Show%20activity%20on) that I found before. And to delete a marker, I needed the `on()` and `removeLayer` methods. 

```js
function petMarker(long, lat) {
  var marker = L.marker([long, lat], {draggable: true}).addTo(map) // add marker to the map
  marker.bindPopup(petName.value, {closeOnClick: false, autoClose: false}).openPopup() // add pet name to the marker and make sure it's open

  marker.on('dblclick', function() {map.removeLayer(marker)}) // double click to remove marker
}
```

Before double clicking:



https://user-images.githubusercontent.com/91745172/232352319-48905a3d-ce95-4e7f-9395-8f6fbf3ad39d.mp4



After double clicking:



[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
