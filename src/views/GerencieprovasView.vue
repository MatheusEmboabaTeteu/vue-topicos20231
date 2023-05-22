<template>
  <h1>Lista de Provas</h1>
  <div style="">
      <h3>Data/hora</h3>
      <input type="datetime-local" id="dataHora" name="dataHora" v-model="dataHora">
      <h3>Descrição</h3>
      <input type="text" v-model="descricao">
      <h3>Peso</h3>
      <input type="text" v-model="peso">
      <button  @click="cadastrar()">Enviar</button>
  </div>    

  <div>
      <table>
          <thead>
              <td>Data/Hora</td>
              <td>Descrição</td>
              <td>Peso</td>
          </thead>
          <tr v-for="prova in prova" :key="prova.id">
            <td>{{ prova.dataHora}}</td>
            <td>{{ prova.descricao }}</td>
            <td>{{ prova.peso }}</td>
          </tr>
          
      </table>
  </div>
</template>

<script>
import axios from 'axios'
import {onMounted, ref} from 'vue'

const prova = ref();
const descricao = ref();
const peso = ref();
const dataHora = ref();

const cadastrar = async () => {

const response = await axios.post('prova', {
  dataHora: dataHora.value,
  descricao: descricao.value,
  peso: peso.value,
},
)
descricao.value = null;
peso.value = null;
dataHora.value = null;
listar()

}

const listar = async () => {
  try {
      let response = await axios.get('prova')
      prova.value = response.data
  } catch (error) {
      
  }
}

export default {
  components: {
    
  },
  data() {
    return {
      prova,
      descricao,
      dataHora,
      peso,
      cadastrar,
      listar
    };
  },
  
  setup() {
    onMounted(() => {
      listar();
    });
  },
};
</script>
