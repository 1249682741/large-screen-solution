<template>
  <div class="wrap">
    <div class="ScaleBox" ref="ScaleBox" :style="{ width, height }">
      <BigScreen></BigScreen>
    </div>
  </div>
</template>

<script>
import BigScreen from './content'
export default {
  name: 'ScaleBox',
  components: { BigScreen },
  props: {
    width: {
      type: Number,
      default: 1920,
    },
    height: {
      type: Number,
      default: 1080,
    },
  },
  data() {
    return {
      scale: null,
    }
  },
  mounted() {
    this.setScale()
    window.addEventListener('resize', this.setScale)
  },
  methods: {
    getScale() {
      const { width, height } = this
      let ww = window.innerWidth / width
      let wh = window.innerHeight / height
      return ww < wh ? ww : wh
    },
    setScale() {
      this.scale = this.getScale()
      this.$refs.ScaleBox.style.setProperty('--scale', this.scale)
    },
    debounce(fn, delay) {
      let delays = delay || 500
      let timer
      return function () {
        let th = this
        let args = arguments
        if (timer) {
          clearTimeout(timer)
        }
        timer = setTimeout(function () {
          timer = null
          fn.apply(th, args)
        }, delays)
      }
    },
  },
}
</script>

<style>
#ScaleBox {
  --scale: 1;
}
.wrap {
  background: #03133f;
  width: 100%;
  height: 5000px;
}
.ScaleBox {
  /* transform: scale(var(--scale)) translate(-50%, -50%); */
  transform: scale(var(--scale)) translate(-50%, 0);
  /* display: flex; */
  height: 100%;
  /* flex-direction: column; */
  transform-origin: 0 0;
  position: absolute;
  left: 50%;
  top: 50%;
  transition: 0.3s;
  z-index: 999;
}
</style>
