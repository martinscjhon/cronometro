<template>
  <div id="app">
    <h1>Bem-vindo ao meu relógio!</h1>
    <h4 class="timer">{{numero}}</h4>
    
    <div class="container-btn">
      <button class="btn" @click="vai">{{botao}}</button>
      <button class="btn" @click="limparRelogio">LIMPAR</button>
    </div>

    <div class="list" v-show="history.length > 0">
      <ul>
        <li v-for="item in history" :key="item">Você parou em: {{item}}</li>      
      </ul>

      <button class="btn-history btn" @click="limparHistory">Limpar histórico</button>
    </div>
  </div>
   
</template>

<script>  
 
  export default{
    name: "AppComponent", 
    data(){
      return{
        numero: 0,
        timer: null,
        botao: "VAI",
        ss: 0,
        mm: 0,
        hh: 0,
        history: []
      }
    },
    methods: {
      vai(){
       if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
        this.botao = "VAI"     
        
        if(this.ss !== 0){
          this.history.push(this.numero)
        }
       } else {
        
        this.timer = setInterval(() => {
          this.rodarTimer();
        }, 350)
        this.botao = "PAUSAR"
       }
      },

      limparRelogio(){
        if(this.timer !== null){
          clearInterval(this.timer);
          this.timer = null;
          this.numero = 0;
        }

        this.numero = 0;
        this.ss = 0;
        this.mm = 0;
        this.hh = 0;      
        this.botao = "VAI"
      },

      rodarTimer(){
        this.ss++;

        if(this.ss === 59){
          this.ss = 0;
          this.mm++;
        }

        if(this.mm === 59){
          this.mm = 0;
          this.hh++
        }

        let format = 
        (this.hh < 10 ? "0" + this.hh : this.hh) + ":"
        + (this.mm < 10 ? "0" + this.mm : this.mm) + ":"
        + (this.ss < 10 ? "0" + this.ss : this.ss);

        return this.numero = format;
      },

      limparHistory(){
        this.history = [];
      }
    }
  }
</script>

<style scoped>
  #app{
    display: flex;
    flex-direction: column;   
    text-align: center;
  }

  h1{
    color: #fff;
  }

  .timer{
    font-size: 60px;  
    color: #fff; 
    margin-top: 50px; 
  }

  .container-btn{
    margin-top: 50px;   
    display: flex; 
    justify-content: center;
    gap: 13px;
  }

  .btn{
    -webkit-user-select: none;
    width: 100px;
    height: 25px;
    background: transparent;
    border: 1px solid rgb(5, 169, 120);
    cursor: pointer;
    color: #fff;
    border-radius: 5px;    
    font-size: 16px;
  }

  .btn:hover{
    background:rgb(5, 169, 120);
  }

  .list{    
    margin-top: 50px;       
  }

  .list ul{
    list-style: none;        
  }

  .list ul li{    
    list-style: none;
    padding: 10px;
    background: rgb(5, 169, 120);
    border-radius: 30px;    
    color: #fff;    
    margin-top: 8px;
  }

  .list ul li:nth-child(1){
    margin-top: 0;
  }

  .btn-history{
    width: 150px;
    margin-top: 50px;  
    height: 32px;     
  }
</style>