<template>
  <div id="app">
    <h2>Градиентом</h2>
    <div class="container">
      <div class="circle-progress" :style="{background: `conic-gradient(#EBE424 ${progressValue * 360}deg, #4F4466 ${progressValue * 360}deg)`}">
        <div class="circle-progress-w">
            <div class="progress-value">{{ Math.round(progressValue * 100)}}%</div>
        </div>
      </div>
    </div>
    <h2>На SVG</h2>
    <div class="container">
      <div class="val progress-value">{{ Math.round(progressValue * 100)}}%</div>
      <div class="circle-progress1">
        <div class="percent">

            <svg>
              <circle class="circle-outer" cx="120" cy="120" r="100"/>
              <circle class="circle-inner" :style="{'stroke-dashoffset': `calc(440 - ((440 * ${progressValue * 100}) / 100))`}" cx="86" cy="86" r="70"/>

          </svg>

        </div>
      </div>

    </div>
    <input type="range" min="0" max="1" step="0.01" v-model="progressEnd" @input="changeValue($event.target.value)">
    <input type="number" min="0" max="1" step="0.01" v-model="progressEnd" @input="changeValue($event.target.value)">
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data() {
    return {
      progressValue: 0,
      progressEnd: 0,
    }
  },
  methods: {
    changeValue(){
      if(this.progressEnd > 1) {
        this.progressEnd = 0
      }
      let progress = setInterval(() => {
        this.progressValue < this.progressEnd
            ? this.progressValue= +this.progressValue.toFixed(2) + 0.01
            : this.progressValue= +this.progressValue.toFixed(2) - 0.01
        if (+this.progressValue.toFixed(2) == this.progressEnd) {
          clearInterval(progress)
        }
      }, 20)
    }
  }
}
</script>

<style>
*,
*:before,
*:after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: lightgray;
}

.container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 300px;
  width: 300px;
  background: #231540;
}

.circle-progress {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 225px;
  width: 225px;
  background: #4F4466;
  border-radius: 50%;
  transition: all 2s ease;
}

.circle-progress-w {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 180px;
  width: 180px;
  background-color: #231540;
  border-radius: 50%;
  transition: all 2s ease;
}

.progress-value {
  font-size: 36px;
  color: #EBE424;
  text-shadow: -3px -3px 20px #EBE424, 3px 3px 20px #EBE424;
  transition: all 2s ease;
}
input {
  width: 300px;
  margin-top: 30px;
}
input[type=number] {
  width: 80px;
  height: 40px;
  font-size: 24px;
}
svg {
  position: relative;
  width: 250px;
  height: 250px;
  transform: rotate(-85deg);
}
circle {
  width: 100%;
  height: 100%;
  fill: none;
  stroke-width: 20;
  stroke-linecap: round;
  stroke-dasharray: 440;

  stroke: #EBE424;
}
.circle-outer{
  stroke: #4f4466;
  stroke-dasharray: 0;
  stroke-dashoffset: 440;
}
.circle-inner{
  scale: 1.4;
  stroke-width: 17px;
  filter: drop-shadow(1px 1px 3px #EBE424);
}
.val {
  position: absolute;
  top: 44%;
  left: 40%;
}
</style>
