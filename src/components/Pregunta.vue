<template>
  <img 
  v-if="img"
   v-bind:src="img"
   alt="No hay tilin">
  <div class="oscuro"></div>
<div class="pregunta-container">
    
  <input v-model="pregunta" type="text" placeholder="Hazme una pregunta">


    
<p>Recuerda terminar la pregunta con el signo de interrogacion (?)</p>

</div>
<div class="respuesta">
    <h2>{{pregunta}}</h2>
    <h1>{{respuesta}}</h1>
</div>
</template>

<script>
export default {
  data(){
    return {
      pregunta: null,
      respuesta: null,
      img:null
    }
  },
  watch:{
  
    pregunta(value, oldValue){

      console.log({value,oldValue});
      if(!value.includes("?")){
        return;//SALGASE DEL OBSERVADOR
      }
//consumir la api para obtener la respuesta
this.obtenerRespuesta();
    },
  },
  methods:{
    async obtenerRespuesta(){
      this.respuesta="Prensanding...";
      //consumir la api para obtener la respuesta
   const data = await fetch('https://yesno.wtf/api').then(resp=>resp.json());
  console.log(data); 
  const {answer,forced,image} = data;
  console.log(answer);
  this.respuesta = answer;
this.img=image;
  return data;
  
  },
  async prueba(){
    const data2 = await this.obtenerRespuesta(); 
  }
  },
//cada vez que yo llamo atravez de observadores del metodo atravez del ciclo de vida no es necesario el await
}
</script>

<style>

img, .oscuro {
  max-height: 100%;
  max-width:  100%;
  height: 100vh;
  width: 100vw;
  position: fixed;
  top:0px;
  left: 0px;
  z-index: -1;

}
.oscuro{
  background-color: rgba(0, 0, 0, 0.4);
  /*0.0 full transparente, 1.0 full opaco*/
}
.pregunta-container {
  /*para manda al frente */
position: relative;
}
input{
  margin-top: 90px;
  width: 260px;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
}
input:focus{
  outline: none;
}
p,h1,h2{
  color: white;

}
p{
  font-size: 25px;
  margin-top: 0px;
}
.respuesta{
  margin-top: 160px;
}

</style>