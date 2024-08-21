<script>
  export let images;

    // 이미지 슬라이더를 위한 변수&함수 
  let centerIndex = 0;
    $: leftIndex = (centerIndex - 1 + images.length) % images.length;
    $: rightIndex = (centerIndex + 1) % images.length;

  function moveLeft() {
    centerIndex = (centerIndex - 1 + images.length) % images.length;
  }

  function moveRight() {
    centerIndex = (centerIndex + 1) % images.length;
  }
</script>

<div class="slider">
    <img src="{images[leftIndex]}" class="slider-item left" alt="">
    <img src="{images[centerIndex]}" class="slider-item" alt="">
    <img src="{images[rightIndex]}" class="slider-item right" alt="">
    <button class="slider-left-button" on:click={moveLeft}>◀</button>
    <button class="slider-right-button" on:click={moveRight}>▶</button>
</div>

<style>
    
 /* slider */
 .slider {
  position: relative;
  width: 80%;
  margin: 0 10%;
 }
 .slider-item {
  width: 100%;
 }
 .slider-item.left {
  position: absolute;
  top: 0;
  right: 100%;
 }
 .slider-item.right {
  position: absolute;
  top: 0;
  left: 100%;
 }
 .slider-left-button {
  position: absolute;
  top: 50%;
  right: 100%;
 }
 .slider-right-button {
  position: absolute;
  top: 50%;
  left: 100%;
 }
</style>