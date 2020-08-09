<template>
  <h1>Custom Video Player</h1>
  <video
    src="../../assets/videos/gone.mp4"
    id="video"
    class="screen"
    poster="../../assets/img/poster.png"
  ></video>
  <div class="controls">
    <button class="btn" id="play">
      <i class="fa fa-play fa-2x"></i>
    </button>
    <button class="btn" id="stop">
      <i class="fa fa-stop fa-2x"></i>
    </button>
    <input type="range" id="progress" class="progress" min="0" max="100" step="0.1" value="0" />
    <span class="timestamp" id="timestamp">00:00</span>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
@import url('https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css');
/* @import url('../../assets/css/progress.css'); */
</style>