<script>
export default {
  name: 'Clock',

  props: {
    time: {
      type: Date,
      default: new Date()
    }
  },

  data () {
    return {
      light: false
    }
  },

  computed: {
    computeLcdClass: function () {
      return {
        light: (this.light) ? true : false
      }
    }
  },

  methods: {
    onClickLight: function () {
      this.light = !this.light
    }
  }
}
</script>

<template>
  <div class="clock-wrap">
    <div class="clock">
      <div class="clock__btn" @click="onClickLight"></div>
      <div class="clock__body">
        <div class="clock__body__time" :class="computeLcdClass">
          <span class="clock__body__time__text" :class="computeLcdClass">
            <span class="clock__body__time__text__indication">
              {{ this.time | moment('A') }}              
            </span>
            {{ this.time | moment('hh:mm') }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Londrina+Sketch');

.clock-wrap {
  width: 22em;
  margin: auto;
}

@media (max-width: 500px) {
  .clock-wrap {
    width: 20em;
  }
}

.clock {
  text-align: center;
  box-shadow: 20px 38px 34px -26px hsla(0, 0%, 0%, .2);

  &__btn {
    margin: 0;
    display: inline-block;
    height: .8em;
    width: 60%;
    border: 3px solid black;
    border-radius: 5px 90px 225px 80px/0px 225px 100px 255px;
    box-shadow: 0 0 15px hsla(0, 0%, 0%, .2);
  }

  &__body {
    margin: 0;
    border-radius: 20px;
    padding: 1.2rem 1.2em;
    border: 3px solid black;
    border-radius: 255px 15px 225px 15px/15px 225px 10px 255px;

    &__time {
      border-radius: 12px;
      padding-top: .2em;
      padding-bottom: .2em;
      border: 3px solid black;
      border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
      box-shadow: inset 0 0 18px hsla(0, 0%, 0%, .2);

      &__text {
        color: black;
        font-family: 'Londrina Sketch', cursive;
        font-size: 3.5em;
        font-weight: bold;

        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -o-user-select: none;
        user-select: none;
        
        box-shadow: 20px 38px 34px -26px hsla(0,0%,0%,.2);

        &__indication {
          font-size: 70%;
          display: inline-block;
          vertical-align: text-top;
        }
      }

      &__text.light {
        color: white;
      }
    }

    &__time.light {
      background: radial-gradient(circle at center, #6F7C8F, #6D687C);
    }
  }
}
</style>
