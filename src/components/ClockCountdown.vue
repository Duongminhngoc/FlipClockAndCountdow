<template>
  <div class="main">
    <div class="time">
      <div class="time-info">
        <div id="i1" class="time-top">{{ time.days | zerofill }}</div>
        <div id="i11" class="time-top-back" :data-value="time1.days | zerofill"></div>
        <div id="i2" class="time-bottom" :data-value="time.days | zerofill"></div>
        <div id="i22" class="time-bottom-back" :data-value="time1.days | zerofill"></div>
      </div>
      <p>Days</p>
    </div>
    <div class="time">
      <div class="time-info">
        <div id="i3" class="time-top">{{ time.hours | zerofill }}</div>
        <div id="i33" class="time-top-back" :data-value="time1.hours | zerofill"></div>
        <div id="i4" class="time-bottom" :data-value="time.hours | zerofill"></div>
        <div id="i44" class="time-bottom-back" :data-value="time1.hours | zerofill"></div>
      </div>
      <p>Hours</p>
    </div>
    <div class="time">
      <div class="time-info">
        <div id="i5" class="time-top">{{ time.minutes | zerofill }}</div>
        <div id="i55" class="time-top-back" :data-value="time1.minutes | zerofill"></div>
        <div id="i6" class="time-bottom" :data-value="time.minutes | zerofill"></div>
        <div id="i66" class="time-bottom-back" :data-value="time1.minutes | zerofill"></div>
      </div>
      <p>Minutes</p>
    </div>
    <div class="time">
      <div class="time-info">
        <div id="i7" class="time-top ">{{ time.seconds | zerofill }}</div>
        <div id="i77" class="time-top-back" :data-value="time1.seconds | zerofill"></div>
        <div id="i8" class="time-bottom" :data-value="time.seconds | zerofill"></div>
        <div id="i88" class="time-bottom-back" :data-value="time1.seconds | zerofill"></div>
      </div>
      <p>Seconds</p>
    </div>
    <div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ClockCountdown",
  props: {
    msg: String,
  },
  data() {
    return {
      name: "Lion",
      endTime: new Date().getTime() + 36000000,

      time: {
        days: "00",
        hours: "00",
        minutes: "00",
        seconds: "00",
      },
      time1: {
        days: "00",
        hours: "00",
        minutes: "00",
        seconds: "00",
      },
    };
  },
  methods: {
    updateTime() {
      let time = Math.max(this.endTime - new Date().getTime(), 0) / 1000;
      let time1 = Math.max(this.endTime - new Date().getTime(), 0) / 1000 - 1;
      this.time.days = Math.floor(time / 86400);
      this.time.hours = Math.floor((time % 86400) / 3600);
      this.time.minutes = Math.floor(((time % 86400) % 3600) / 60);
      this.time.seconds = Math.floor(((time % 86400) % 3600) % 60);
      this.time1.days = Math.floor(time1 / 86400);
      this.time1.hours = Math.floor((time1 % 86400) / 3600);
      this.time1.minutes = Math.floor(((time1 % 86400) % 3600) / 60);
      this.time1.seconds = Math.floor(((time1 % 86400) % 3600) % 60);
    },
  },
  watch: {
    "time.seconds": function () {
      let element = document.getElementById("i7");
      setTimeout(function () {
        element.classList.add("animation1");
      }, 500);

      setTimeout(function () {
        element.classList.remove("animation1");
      }, 1000);
    },
    "time1.seconds": function () {
      let element = document.getElementById("i88");
      setTimeout(function () {
        element.classList.add("animation2");
      }, 500);

      setTimeout(function () {
        element.classList.remove("animation2");
      }, 1000);
    },
  },
  filters: {
    zerofill: function (value) {
      return (value < 10 && value > -1 ? "0" : "") + value;
    },
  },
  mounted() {
    setInterval(() => this.updateTime(), 1000);
  },
  beforeDestroy() {
    clearInterval(this.updateTime);
  },
};
</script>

<style lang="scss" scoped>
.main {
  display: flex;
  flex-direction: row;
  justify-content: center;
  .time {
    margin: 0px;
    .time-info {
      position: relative;
      width: 100px;
      height: 100px;
      font-size: 90px;
      font-weight: 600;
      color: #fff;
      margin: 5px;
      .time-top {
        background-color: rgb(46, 44, 44);
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
        height: 50%;
        transform-style: preserve-3d;
      }
      .animation1 {
        animation: flipTop .5s;
        animation-fill-mode: both;
        transform-origin: center bottom;

      }
      .time-top-back {
        background-color: rgb(46, 44, 44);
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
        height: 50%;
        &::after {
          content: attr(data-value);
          display: block;
          margin-top: -50%;
        }
      }
      .time-bottom {
        position: absolute;
        height: 50%;
        top: 50%;
        overflow: hidden;
        z-index: 2;
        background-color: rgb(92, 86, 86);
        border-radius: 0 0 10px 10px;
        border-top: 1px black solid;
        
        &::after {
          content: attr(data-value);
          display: block;
          margin-top: -50%;
        }
      }
      .animation2 {
        animation: flipBottom 0.5s;
      }
      .time-bottom-back{
        position: absolute;
        height: 50%;
        top: 50%;
        overflow: hidden;
        background-color: rgb(92, 86, 86);
        border-radius: 0 0 10px 10px;
        &::after {
          content: attr(data-value);
          display: block;
          margin-top: -50%;
        }
      }
      @keyframes flipTop {
        0% {
            opacity: 1;
            transform: rotateX(0deg);
            transform-origin: bottom ;
        }
        50% {
            opacity: 1;
            transform: rotateX(45deg);
            transform-origin: bottom ;
        }
        51% {
            opacity: 0;
        }
        100% {
            opacity: 0;
            transform: rotateX(90deg);
            transform-origin: bottom ;
        }
      }
      @keyframes flipBottom {
        0% {
            opacity: 1;
            transform: rotateX(90deg);
            transform-origin: top ;
            z-index: -4;
        }
        50% {
            opacity: 1;
            transform: rotateX(90deg);
            transform-origin: top ;
            z-index: -4;
        }
        51% {
            opacity: 1;
            z-index: 5;
            
        }
        100% {
            opacity: 1;
            transform: rotateX(0deg);
            transform-origin: top ;
            z-index: 5;
        }
      }
    }
  }
}
</style>
