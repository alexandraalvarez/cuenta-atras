<!-- -->
<template>
  <div id="app" class="text-center">
    <div class="title">
      <h1 class="text-center my-3 display-4 italic font-weight-bold">{{message}}</h1>
    </div>
    <div class="time">
      <h2>{{time}} seg/min</h2> 
    </div>
    <div class="buttons">
      <button class="btn btn-outline-dark mx-4 my-4" @click="count(3)">3s</button>
      <button class="btn btn-outline-dark mx-4 my-4" @click="count(60)">1m</button>
      <button class="btn btn-outline-dark mx-4 my-4" @click="count(300)">5m</button>
      <button class="btn btn-outline-dark mx-4 my-4" @click="count(600)">10m</button>
      <button class="btn btn-outline-dark mx-4 my-4" @click="count(1800)">30m</button>
    </div>
  </div>
</template>

<script>
let interval;
  export default {

    name: "contador",
    data() {
      return {
        message: 'Cuenta atrás',
        time: "00:00",
      };
    },

    methods:{
    count: function (seg) {  //tiempo actual + tiempo de descuento
      clearInterval(interval);
      const now = Date.now();
      const end = now + (seg + 1) * 1000;
      this.descontar(end);
    },

     
    descontar: function (end) { //tiempo restante
      interval = setInterval(() => {
        const leftTime = Math.round((end - Date.now()) / 1000);

        if (leftTime < 0) {
          clearInterval(interval);
          return;
        }
        
        const minutes = Math.floor((leftTime % 3600) / 60);
        const seconds = leftTime % 60;
        console.log(minutes, seconds);

        //lo que se muestra en el contador
        if (String(seconds).length === 1 && String(minutes).length === 1) {
          this.time = `0${minutes}:0${seconds}`;
        } else if (
          String(seconds).length === 1 &&
          String(minutes).length != 1
        ) {
          this.time = `${minutes}:0${seconds}`;
        } else if (
          String(seconds).length != 1 &&
          String(minutes).length === 1
        ) {
          this.time = `0${minutes}:${seconds}`;
        } else {
          this.time = `${minutes}:${seconds}`;
        }
      }, 1000);
    }
  }
}
</script>
<style scoped>
  #app {
    background-color:  #6AF7E0;;
    border: #000000 solid 3px;
    width: 50%;
    margin: 10% auto;
  }

  .btn{
    color: #000000;
    background-color: #F7E6A2 ;
    border-color: #AE9324;
  }

  .btn:hover{
    background-color:#AE9324;
    color: #FFFFFF;
  }
</style>