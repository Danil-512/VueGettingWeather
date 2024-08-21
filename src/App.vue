<script>
import axios from 'axios'

// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    }
  },
  computed: {
    cityName() {
      return this.city + "?"
    },
    cityTemp() {
      return "Температура " + this.info.main.temp + "°C"
    },
    cityFeelsLikeTemp() {
      return "Ощущается как " + this.info.main.temp + "°C"
    },
    cityMinTemp() {
      return "Минимальная температура " + this.info.main.temp + "°C"
    },
    cityMaxTemp() {
      return "Максимальная температура " + this.info.main.temp + "°C"
    }
    
  },
  methods: {
    getWeather() {
      // alert("Some")
      // Функция trim позволяет обрезать лишние пробелы до и после строки
      if(this.city.trim().length < 3) {
        this.error = "Слишком мало символов"
        return false
      }
      // else {
      //   this.error = ""
      //   return false
      // }
      this.error = ""

      // `` - отформатированная строка
      // axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=a2ce3a846201aa4ca9be7ad6a803029f`)
      //   .then(res => (this.info = res))
      // Записываем в info то, что получили в качестве ответа в res
      // () => {}

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=London&units=metric&appid=a2ce3a846201aa4ca9be7ad6a803029f`)
        .then(res => (this.info = res.data))
    }
  }
}

</script>

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main> -->
  <div class="wrapper">
    
    <h1>Погода в твоем городе</h1>
    
    <p>Узнать актуальную погоду в <span class="color1">{{ city == "" ? "X" : cityName}}</span></p>

    <p>
      <!-- <input type="text" v-on:input="this.city = $event.target.value" placeholder="Введите город"> -->
      <!-- v-on:input="" Функция на обработчик событий из библиотек вью. Код в "" срабатывает каждый
       раз при вводе символа. $event.target.value - получает значение самого инпут поля -->

      <!-- <input type="text" @input="this.city = $event.target.value" placeholder="Введите город"> -->
      <input type="text" v-model="city" placeholder="Введите город">
      <!-- <p><span>ㅤ</span><button v-show="city != ''">Получить результат</button><span>ㅤ</span></p> -->
      <p><span>ㅤ</span><button v-if="city != ''" @click="getWeather()">Получить результат</button>
      <button disabled v-else>Введите название города</button><span>ㅤ</span></p>
      <!-- v-show="" Если условие корректно, элемент показывается -->
      <!-- v-if показывает элемент, если условие корректно -->
      
      
      

    </p>
    <p class="error">{{ error }}</p>
    
    <!-- <p v-if="info !=null">{{ info }}</p> -->
    <!-- <p v-show="info != null">{{ cityTemp }}</p> -->
<!--  -->

    <div v-show="city != ''">
      <div v-if="info != null" class="info-block">
          <p>Погода в городе {{ city }}</p>
          <p>{{ cityTemp }}</p>
          <p>{{ cityMaxTemp }}</p>
          <p>{{ cityMinTemp }}</p>
          <p>{{ cityFeelsLikeTemp }}</p>
      </div>
    </div>
    
    
    


  </div>
  <!-- <iframe src="https://youtu.be/TiBCLraUFvA" frameborder="0"></iframe> -->
  
 


</template>

<style scoped>

.info-block p {
  margin: 10px;

}

.info-block {
  width: 20vw;
  background: rgba(0, 0, 0, 0.15);  ;
  display: inline-block;
  text-align: center;
  border-radius: 5px;
  color: rgba(128, 254, 183, 0.674);

  padding-top: 5px;
  padding-bottom: 5px;


}


.json {
  height: 80vh;
  width: 80vw;
}

.error {
  color: rgba(255, 0, 0, 0.434);
  text-shadow: 
    /* -1px -1px 0 black,
    1px -1px 0 black,
    -1px 1px 0 black,*/
    1px 1px 0 rgba(0, 0, 0, 0.616);  ;
}

.color1 {
  color: rgba(128, 254, 183, 0.674);
}

.wrapper {
  min-width: 640;
  min-height: 480px;
  max-width: 3840px;
  max-height: 2160px;
  /* display: flex; */

  width: 85vw;
  height: 80vh;

  border-radius: 50px;
  background-color: rgba(64, 57, 137, 0.6);
  text-align: center;
  padding: 20px;
  color: rgba(255, 255, 255, 0.663);

  /* display: flex;
  flex-direction: column;
  justify-content: center;
   */
  /* background: #111; */
}

.wrapper>p {
  /* margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto; */
  margin-top: 15px;
}

 .wrapper>h1 {
  margin-top: 25vh;
  /* margin-bottom: 15px; */
} 

.wrapper input {
  /* color: rgba(64, 57, 137, 0.6);; */
  background: transparent;
  border: 0px;
  border-bottom: 1px solid rgba(128, 254, 183, 0.511);;
  font-weight: bold;

  /* Я хз почему цвет текста не меняется */
  color: rgba(255, 255, 255, 0.438);
  /* Получилось обратившись к плейсхолдеру */

  padding: 2px 4px;

  /* Обводка */
  outline: none;

}

.wrapper ::placeholder {
  color: rgba(255, 255, 255, 0.438);
}

.wrapper p>button {
  /* margin-left: 10px; */
  background: rgb(161, 168, 204);
  color: rgb(255, 255, 255);
  border-radius: 5px;
  padding: 4px 6px;
  border-color: rgba(128, 254, 183, 0.511);
  /* margin-left: 15px; */
  margin-top: 20px;

  cursor: pointer;

  transition: transform 500ms ease;
}

.wrapper button:disabled {
  background: rgba(64, 57, 137, 0.196);
  cursor: not-allowed;
}

.wrapper button:hover {
  /* Эффект пр наведении  */
  transform: scale(1.1) translateY(-5px);
}



.wrapper input:focus {
  /* Эффект при нажатии */

  /* border-bottom-color: rgba(0, 0, 0, 0.27); */
  /* color: rgba(128, 254, 183, 0.531); */
  
  color: rgba(128, 254, 183, 0.511);
  border-color: rgba(128, 254, 183, 0.75);

  
  
}










/* header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */


</style>
