# Entry 3
##### 02/12/23

I followed this [youtube video](https://www.youtube.com/watch?v=OYjFR_CGV8o&list=PLGHe6Moaz52PUNP4DtIshALDogSURIlYB&index=3) to learn how to make circles and polygons on my map. When I started to do the circle, a regular marker appeared. At first, everything looked good and I followed what the video did. Then, I realized that instead of `L.circle` I wrote `L.marker`. I tinkered with the `fillColor` of the circle and found out that the color inside the circle is the same as the circle's border (just a little lighter). So you don't really need it unless you want the color inside the circle to be different.

``` js
var circle = L.circle([51.508, -0.11], {
  color: 'red',
  fillColor: 'red',
}
```

OR

``` js
var circle = L.circle([51.508, -0.11], {
  color: 'red',
}
```

![image](https://user-images.githubusercontent.com/91745172/218330489-1685ea5e-7063-4775-9c77-1d2c180bd5b6.png)


``` js
var circle = L.circle([51.508, -0.11], {
  color: 'red',
  fillColor: 'green',
}
```
![image](https://user-images.githubusercontent.com/91745172/218330591-f803d765-7e19-4ab0-98c7-0d8fc04c26a1.png)

Then I moved on to a polygon. I added a popup to the polygon and I noticed that I can't open both the polygon and the smiley face popup at the same time because one of them would close if I open the other one.

![polygon popup](https://user-images.githubusercontent.com/91745172/218325282-7ef1a5b1-dbf8-4042-ac37-80a1f4b40d05.png)
![smileyface popup](https://user-images.githubusercontent.com/91745172/218325304-4a979ed3-16f5-4140-8ed4-3428a1d93cf1.png)

I didn't want the popups to close so I googled "Can you open multiple popups at the same time leaflet Stack overflow." As I was scrolling on [Stack Overflow](https://stackoverflow.com/questions/38957585/how-can-i-open-multiple-popups-in-leaflet-marker-at-a-time), I saw `{closeOnClick: false, autoClose: false}` and decided to use it. I added it to both the polygon and the smiley face marker.

``` js
// smiley popup
marker.bindPopup("Hello!!",{closeOnClick: false, autoClose: false})

// polygon popup
polygon.bindPopup("I'm a polygon", {closeOnClick: false, autoClose: false})
```

![polygon and smiley face img](https://user-images.githubusercontent.com/91745172/218325234-4afb66ce-ec28-4d9c-b3e3-9bc91c1bdc90.png)

I followed this [youtube video](https://www.youtube.com/watch?v=wnsEYm9hF0o&list=PLGHe6Moaz52PUNP4DtIshALDogSURIlYB&index=4&ab_channel=MapTiler) to add a shadow to the smiley face, circle, and polygon. After watching the video, I was still confused about the value of `iconAnchor` and `shadowAnchor` because the guy didn't specify how to get those values. I googled "how to find the value of iconAnchor leaflet js," but I couldn't find anything helpful. So I'm planning to learn about the anchor values next. I'm also planning to learn how to add [GeoJSON](RIlYB&index=5&ab_channel=MapTiler), [scale and watermarks](https://www.youtube.com/watch?v=SfBkBBM4U8U&list=PLGHe6Moaz52PUNP4DtIshALDogSURIlYB&index=6&ab_channel=MapTiler) with the same youtube channel.

I’m currently in the research the problem stage in the engineering design process.

The three skills that I’m developing are how to google, how to read, and attention to detail. I had to google how to make the popups not close when I open a different popup. I found the answer on Stack Overflow and had to read carefully through all the code and find what I needed. I had to pay attention to detail when a regular marker appeared instead of a circle because I had written something wrong in my code.

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
