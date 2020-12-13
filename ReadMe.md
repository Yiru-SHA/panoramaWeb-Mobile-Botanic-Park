Question：

I want to add HotSpot in someplace, and show one image or one video after mouse click on it.

<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>360&deg; Image Gallery</title>
    <meta name="description" content="360&deg; Image Gallery - A-Frame">
    <script src="https://aframe.io/releases/1.0.4/aframe.min.js"></script>
    <script src="https://unpkg.com/aframe-event-set-component@5/dist/aframe-event-set-component.min.js"></script>
    <script src="https://unpkg.com/aframe-layout-component@5.3.0/dist/aframe-layout-component.min.js"></script>
    <script src="https://unpkg.com/aframe-template-component@3.2.1/dist/aframe-template-component.min.js"></script>
    <script
        src="https://unpkg.com/aframe-proxy-event-component@2.1.0/dist/aframe-proxy-event-component.min.js"></script>
    <!-- mouse control-->
    <script src="https://cdn.jsdelivr.net/gh/donmccurdy/aframe-extras@v6.1.1/dist/aframe-extras.min.js"></script>

    <!-- Image link template to be reused. -->
    <!-- geometry是缩略图的尺寸 -->
    <script id="link" type="text/html">
      <a-entity class="link"
        geometry="primitive: plane; height: 1; width: 1"
        material="shader: flat; src: ${thumb}"
        event-set__mouseenter="scale: 1.2 1.2 1"
        event-set__mouseleave="scale: 1 1 1"
        event-set__click="_target: #image-360; _delay: 300; material.src: ${src}"
        proxy-event="event: click; to: #image-360; as: fade"
        sound="on: click; src: #click-sound"></a-entity>
  </script>
</head>

<body>
        <a-scene>
            <!-- preload 加载图片和声音 -->
            <a-assets>
                <img id="city" crossorigin="anonymous" src="panorama01.jpg">
                <img id="city-thumb" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/thumb-city.jpg">
               
                <img id="cubes-thumb" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/thumb-cubes.jpg">
                <img id="cubes" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/cubes.jpg">

                <img id="sechelt-thumb" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/thumb-sechelt.jpg">
                <img id="sechelt" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/sechelt.jpg">

                <audio id="click-sound" crossorigin="anonymous"
                    src="https://cdn.aframe.io/360-image-gallery-boilerplate/audio/click.ogg"></audio>
                
            </a-assets>
            <a-assets>
                <audio id="bgMusic" src="song.mp3" preload="auto"></audio>
                <video id="penguin-sledding" autoplay loop="true" src="penguin-sledding.mp4"></video>
            </a-assets>

            
            <!-- <a-video src="#penguin-sledding" width="16" height="9" position="0 0 -20"></a-video>
            <a-video src="airbending.mp4"></a-video> -->


            <!-- 360-degree image. 第一个显示在页面上的全景图-->
            <a-sky id="image-360" radius="10" src="#city"
                animation__fade="property: components.material.material.color; type: color; from: #FFF; to: #000; dur: 300; startEvents: fade"
                animation__fadeback="property: components.material.material.color; type: color; from: #000; to: #FFF; dur: 300; startEvents: animationcomplete__fade">
            </a-sky>

            <!-- Image links. -->
            <a-entity id="links" layout="type: line; margin: 1.5" position="0 -1 -4">
                <a-entity template="src: #link" data-src="#cubes" data-thumb="#cubes-thumb"></a-entity>
                <a-entity template="src: #link" data-src="#city" data-thumb="#city-thumb"></a-entity>
                <a-entity template="src: #link" data-src="#sechelt" data-thumb="#city-thumb"></a-entity>

            </a-entity>

            <!-- Camera + cursor. -->
            <!-- <a-entity movement-controls="speed: 0.15" position=" 0 0 6"> -->


            <a-entity camera look-controls>
                <a-cursor id="cursor"
                    animation__click="property: scale; startEvents: click; from: 0.1 0.1 0.1; to: 1 1 1; dur: 150"
                    animation__fusing="property: fusing; startEvents: fusing; from: 1 1 1; to: 0.1 0.1 0.1; dur: 1500"
                    event-set__mouseenter="_event: mouseenter; color: springgreen"
                    event-set__mouseleave="_event: mouseleave; color: black" raycaster="objects: .link"></a-cursor>
            </a-entity>

            <a-entity colorHostpot></a-entity>
           

            <!-- test for play music -->
            <!-- <a-entity sound="src: #bgMusic; autoplay: true" volume="0.2"></a-entity> -->
        </a-scene>
<!--         
        <aside> how to add HotSpot which will be shown in front of the 360 image
            <div>
                <button>click me!!</button>
            </div>

        </aside> -->

    <!--通过给link标注id和type来关联html中的script和app的script-->
    <!-- <script src="app.js"></script> -->
</body>

</html>