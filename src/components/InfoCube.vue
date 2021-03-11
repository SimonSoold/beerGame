<template>
<div class="scene">
  <div class="cube">
    <div class="cube__face cube__face--front">front</div>
    <div class="cube__face cube__face--back">back</div>
    <div class="cube__face cube__face--right">right</div>
    <div class="cube__face cube__face--left">left</div>
    <div class="cube__face cube__face--top">top</div>
    <div class="cube__face cube__face--bottom">bottom</div>
  </div>
</div>
</template>

<script>
export default {

}
</script>

<style>
.scene {
  width: 100%;
  height: 100%;
  perspective: 385px;
  transform: rotate(90deg);
}

.cube {
  width: 200px;
  height: 200px;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(65deg) rotateZ(270deg) rotateY(270deg); 
}

.cube__face {
  position: absolute;
  width: 200px;
  height: 200px;
  
}

.cube__face--front  { 
  transform: rotateY(  0deg) translateZ(100px); 
    background: blue;
  }
.cube__face--right  { 
  transform: rotateY( 90deg) translateZ(100px); 
      background: rgb(96, 96, 182);
  }
.cube__face--back   { 
  transform: rotateY(180deg) translateZ(100px); 
        background: rgb(84, 84, 219);
  }
.cube__face--left   { 
  transform: rotateY(-90deg) translateZ(100px); 
          background: rgb(45, 45, 177);
  }
.cube__face--top    { 
  transform: rotateX( 90deg) translateZ(100px); 
      background: rgb(8, 8, 202);
  }
.cube__face--bottom { 
  transform: rotateX(-90deg) translateZ(100px); 
        background: rgb(31, 31, 189);
  }
</style>