<template>
  <h2>{{titulo || 'txr que necesito'}}</h2>
  <p>{{ numero }} <sup>2</sup>={{ calcular }}</p>

  <div>
    <button @click="incrementar">+1</button>

    <button @click="dismunuir">-1</button>
  </div>
</template>

<script>
export default {
  props: ["titulo","numero"],

  data() {
    return {
      numero: 5,
    };
  },
  methods: {
    calcularCuadrado() {
      console.log("Ingreso al metodo");
      return this.numero * this.numero;
    },
    calcularCuadrado2(num1, num2) {
      return num1 * num2;
    },
    incrementar() {
      this.numero++;
    },
    dismunuir() {
      this.numero--;
    },
  },
  computed: {
    calcular() {
      console.log("Ingreso a la propiedad computada");
      return this.numero * this.numero;
    },
    presentar(){
      if(this.titulo != undefined){
       return this.titulo

      }else{
        return "Texto que quiero"
      }
    },
  },
};
</script>

<style>
button {
  background: #64b687;
  border-radius: 5px;
  border: 1px solid white;
  color: black;
  margin: 0px 5px;
  padding: 5px 10px;
  cursor: pointer;
}
button:hover {
  background-color: #5aa67b;
}
</style>