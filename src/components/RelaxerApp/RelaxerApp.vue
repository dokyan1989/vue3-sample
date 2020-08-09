<template>
  <div class="relaxer-body">
    <h1>Relaxer</h1>

    <div class="container" v-bind:class="breatheClass">
      <div class="circle"></div>

      <p>{{ text }}</p>

      <div class="pointer-container">
        <div class="pointer"></div>
      </div>

      <div class="gradient-circle"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RelaxerApp',
  data() {
    return {
      text: '',
      totalTime: 7500,
      isGrow: true,
      breatheIntervalId: 0,
    }
  },
  computed: {
    breatheTime() {
      return (this.totalTime / 5) * 2
    },
    holdTime() {
      return this.totalTime / 5
    },
    breatheClass() {
      return this.isGrow ? 'grow' : 'shrink'
    },
  },
  mounted() {
    this.breatheAnimation()
    this.breatheIntervalId = setInterval(
      () => this.breatheAnimation(),
      this.totalTime
    )
  },
  beforeUnmount() {
    clearInterval(this.breatheIntervalId)
  },
  methods: {
    breatheAnimation() {
      this.text = 'Breath In!'
      this.isGrow = true

      setTimeout(() => {
        this.text = 'Hold'

        setTimeout(() => {
          this.text = 'Breathe Out!'
          this.isGrow = false
        }, this.holdTime)
      }, this.breatheTime)
    },
  },
}
</script>

<style scoped>
.relaxer-body {
  background: #224941 url('../../assets/img/bg.jpg') no-repeat center
    center/cover;
  color: #fff;
  font-family: 'Montserrat', sans-serif;
  min-height: 100vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: auto;
  height: 300px;
  width: 300px;
  position: relative;
  transform: scale(1);
}

.circle {
  background-color: #010f1c;
  height: 100%;
  width: 100%;
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}

.gradient-circle {
  background: conic-gradient(
    #55b7a4 0%,
    #4ca493 40%,
    #fff 40%,
    #fff 60%,
    #336d62 60%,
    #2a5b52 100%
  );
  height: 320px;
  width: 320px;
  z-index: -2;
  border-radius: 50%;
  position: absolute;
  top: -10px;
  left: -10px;
}

.pointer {
  background-color: #fff;
  border-radius: 50%;
  height: 20px;
  width: 20px;
  display: block;
}

.pointer-container {
  position: absolute;
  top: -40px;
  left: 140px;
  width: 20px;
  height: 190px;
  animation: rotate 7.5s linear forwards infinite;
  transform-origin: bottom center;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.container.grow {
  animation: grow 3s linear forwards;
}

@keyframes grow {
  from {
    transform: scale(1);
  }

  to {
    transform: scale(1.2);
  }
}

.container.shrink {
  animation: shrink 3s linear forwards;
}

@keyframes shrink {
  from {
    transform: scale(1.2);
  }

  to {
    transform: scale(1);
  }
}
</style>