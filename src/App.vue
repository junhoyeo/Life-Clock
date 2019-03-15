<script>
import moment from 'moment'
import Clock from '@/components/Clock'
import Grave from '@/components/Grave'

export default {
  name: 'app',
  components: {
    Clock,
    Grave
  },
  
  created: function () {
    this.age = Number(this.$cookie.get('age'))
    this.life = Number(this.$cookie.get('life'))

    if (!this.age || !this.life) {
      this.age = this.life = 0
    } else this.show = true
  },

  data: function () {
    return {
      show: false,
      birth: '0000-00-00',
      death: '0000-00-00',
      time: new Date(),
      age: 0,
      life: 0
    }
  },

  methods: {
    getDate: function (timestring) {
      return new Date(timestring)
    },
    
    getDiff: function (base) {
      let diff = base - new Date(this.birth)
      return Math.abs(new Date(diff).getUTCFullYear() - 1970);
    },

    getTime: function () {
      return moment().set('hours', (this.age / this.life) * 24)
    },

    updateAge: function () {
      this.age = this.getDiff(new Date)
      this.life = this.getDiff(this.getDate(this.death))
    },

    selectAge: function (age) {
      let dt = this.getDate(this.birth)
      this.death = new Date(dt.setFullYear(dt.getFullYear() + age)).toISOString().slice(0, 10)
      this.updateAge()
    },

    selectInfo: function () {
      this.$cookie.set('age', this.age, { expires: '1Y' });
      this.$cookie.set('life', this.life, { expires: '1Y' });
      this.show = true
    }
  }
}
</script>

<template>
  <div id="app">
    <div id="info" v-if="!show">
      <h1>먼저, 간단한 정보를 입력해 주세요.</h1>
      <div class="form">
        <h2 class="form__title">당신의 생년월일</h2>
        <input class="form__input" type="date" v-model="birth" @keypress="updateAge" max="2999-12-31"/>
        <h2 class="form__title">당신의 예상 사망일</h2>
        <input class="form__input" type="date" v-model="death" @keypress="updateAge"/>
      </div>

      <Grave 
        :birth="birth.slice(0, 4)" 
        :death="death.slice(0, 4)" 
        :age="life"
      />

      <div class="age-btn" v-if="birth != '0000-00-00'">
        <span class="age-btn__button" 
          v-for="(age, idx) in [80, 90, 100, 120, 140]" :key="idx"
          @click="selectAge(age)"
        >
          {{ age }}
        </span>
      </div>

      <div class="btn-next" @click="selectInfo">입력 완료</div>
    </div>
    <div id="clock" v-else>
      <h1>당신의 삶에는 아직 해도 뜨지 않았어요</h1>
      <Clock :time="getTime()" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Nanum+Brush+Script');

#app {
  font-family: 'Nanum Pen Script', cursive;

  h1 {
    margin-top: 1.5em;
    font-size: 3.5em;
    font-weight: lighter;
    text-align: center;
    user-select: none;
  }
}

#clock {
  margin-top: 2.5em;  
}

#info {
  text-align: center;

  h1 {
    margin-top: 1em;
  }

  .btn-next {
    margin: auto;
    margin-top: 1em;
    user-select: none;
    width: 10%;
    font-size: 2em;
    border: 3.5px solid black;
    border-radius: 255px 15px 225px 15px/15px 225px 10px 255px;    

    @media (max-width: 700px) {
      width: 30%;
    }
  }

  .form {
    &__title {
      margin: 0;
      font-size: 2.2em;
    }

    &__input {
      font-size: 3em;
    }
  }

  .age-btn {
    margin-top: 1em;

    &__button {
      font-size: 1.5rem;
      padding-left: 5px;
      padding-right: 3px;
      border: 2px solid black;
      border-radius: 25px;
    }
  }

  .grave-wrap {
    margin-top: 2em;
  }
}
</style>
