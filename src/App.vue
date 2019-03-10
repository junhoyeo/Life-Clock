<script>
import Clock from '@/components/Clock'

export default {
  name: 'app',
  components: {
    Clock
  }
}
</script>

<template>
  <div id="app">
    <h1>당신의 삶에는 아직 해도 뜨지 않았어요</h1>
    <Clock/>
  </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Nanum+Brush+Script');

#app {
  margin-top: 5em;

  h1 {
    font-family: 'Nanum Brush Script', cursive;
    font-size: 3.5em;
    font-weight: lighter;
    text-align: center;
    margin-bottom: 2.5em;

    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -o-user-select: none;
    user-select: none;
  }
}
</style>
