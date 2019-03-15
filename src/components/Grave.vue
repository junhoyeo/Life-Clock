<script>
export default {
  name: 'Clock',

  props: {
    birth: {
      type: String,
      default: ''
    },
    death: {
      type: String,
      default: ''
    },
    age: {
      type: Number,
      default: 0
    }
  }
}
</script>


<template>
  <div class="grave-wrap">
    <div class="grave">
      <div class="grave__stone">
        <span class="grave__stone__span" v-if="birth">{{ birth }} ~ {{ death }}</span>
        <span class="grave__stone__dead" v-if="age">{{ age }} 세</span>
      </div>
      <div class="grave__base"/>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Nanum+Pen+Script');

.grave-wrap {
  width: 100%;
}
.grave {
  width: 20em;
  margin: auto;
  text-align: center;
  font-family: 'Nanum Pen Script', cursive;
  font-size: 1.5em;
  user-select: none;

  &__stone {
    margin: auto;
    height: 10em;
    width: 30%;
    border: 3px solid black;
    border-radius: 255px 100px 225px 15px/100px 100px 10px 255px;
    box-shadow: 8px 10px 10px -5.5px hsla(0,0%,0%,.2);
    
    span {
      font-size: 1.2em;
    }

    &__span {
      display: block;
      margin-top: 2.5em;
    }

    &__dead {
      display: block;
      margin-top: 1em;
    }
  }

  &__base {
    margin: auto;
    margin-top: -3px;
    height: 1em;
    width: 40%;
    border: 3px solid black;
    border-radius: 15px 100px 225px 15px/12px 100px 15px 255px;
    box-shadow: 25px 10px 20px -10px hsla(0,0%,0%,.2);
  }
}
</style>
