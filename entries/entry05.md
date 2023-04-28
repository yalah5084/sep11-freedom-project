# Entry 5
##### 04/27/23

#### Tinker with tool

I followed this [Youtube tutorial](https://www.youtube.com/watch?v=SfBkBBM4U8U&list=PLGHe6Moaz52PUNP4DtIshALDogSURIlYB&index=7&ab_channel=MapTiler) to see how I can add a scale. It was really simple, I only needed 5 lines of code. When I saw the scale, I actually didn't know what it meant. I didn't know what it was measuring. I google how a scale works in Leaflet js, then the internet said "Scale shows the scale which applies to the center point of the map." I was thinking to use the scale for my freedom project, but after what I found on the internet, I didn't think the scale was useful.

```js
L.control.scale({
  metric: true,
  imperia: false,
  position: 'bottomright'
}).addTo(map)
```

While I was scrolling through the reference, [PosAnimation](https://leafletjs.com/reference.html#posanimation) caught my eyes. I copied the example and see what kind of animation it was. Turns out it makes the marker bounce when you click on it.

```js
var myPositionMarker = L.marker([48.864716, 2.294694]).addTo(map);

myPositionMarker.on("click", function() {
    var pos = map.latLngToLayerPoint(myPositionMarker.getLatLng());
    pos.y -= 40;
    var fx = new L.PosAnimation();

    fx.once('end',function() {
        pos.y += 40;
        fx.run(myPositionMarker._icon, pos, 0.8);
    });

    fx.run(myPositionMarker._icon, pos, 0.3);
});
```

I changed the values to see how it would affect the marker. I tried to understand every line of code and realized it used the concept of object which I had have seen a little in class. I'm still not really familiar with objects, but I somewhat understood what every line of code did execept the last one because I didn't know what the `0.3` was. After changing the `0.8` to `0` and changing `0.3` to `5`, I understood that the last line of code is the time it takes the marker to go up. I `console.log(pos.y)` before and after `pos.y -= 40` and `pos.y += 40` to see how the y changes. I `console.log(map.latLngToLayerPoint(myPositionMarker.getLatLng()))` to see what it was. I also looked through the reference to see what `latLngToLayerPoint()` and `getLatLng()` were. I read that it's about the geographical position of the marker and the pixel coordinate. It was easier than I expected to understand the code.


https://user-images.githubusercontent.com/91745172/235046322-107b5c33-5b13-46ad-899d-fd64c529674d.mp4


#### MVP + Beyond MVP

I added another box for the user to provide a short description of the lost pet. I stored the HTML element in a variable called `description` and the value of it with the pet's name.

```js
var description = document.getElementById('description')
...
function petMarker(long, lat) {
  marker.bindPopup(petName.value + "<br>" + description.value, {closeOnClick: false, autoClose: false}).openPopup() // add pet name to the marker and make sure it's open
}
```

https://user-images.githubusercontent.com/91745172/235048347-d6f45996-07f5-4e8b-ab2a-9c9c98a07e80.mp4


I wanted to make the marker bounce when it was clicked like I learned when tinkering with my tool. I followed the same way it was written in the example. I changed the speed, time and the variable names. 

```js
function petMarker(long, lat) {
  var marker = L.marker([long, lat], {draggable: true}).addTo(map) // add marker to the map
   // make marker bounce
  marker.on("click", function() {
    var pos = map.latLngToLayerPoint(marker.getLatLng());
    pos.y -= 20;
    var y = new L.PosAnimation();

    y.once('end',function() {
        pos.y += 20;
        y.run(marker._icon, pos, 0.5); // go down time
    });

    y.run(marker._icon, pos, 0.5); // go up time
  });
}
```

https://user-images.githubusercontent.com/91745172/235050353-91f15e9d-e647-43c2-9698-b310d36af789.mp4

I'm currently in the create a prototype stage in the engineering design process. I finished creating my MVP and added an extra thing the project. The next stage will be to test and evaluate the prototype in order to improve as needed and add more things.

Three skills I developed are how to learn, problem decomposition and how to read. I watched a Youtube video on how to add a scale on the map. I used Leaflet's reference to learn about `PosAnimation` and carefully read the table to help me understand the example. I broke down the example into smaller pieces in order to understand what every line of code does and how it makes the marker bounce.



[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
