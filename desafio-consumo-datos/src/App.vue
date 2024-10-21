<script>
import formchat from './components/form.vue';
import chat from './components/Chat.vue';
import axios from 'axios';

export default {
  components: {
    formchat,
    chat,
  },
  data() {
    return {
      users: [],
      messages: [],
      selectedUsers: [],
    };
  },
  //conexion a la api
  async mounted() {
    try {
      const url = "https://randomuser.me/api/?results=20"; //trae 20 usuarios
      const { data } = await axios.get(url);
      this.users = data.results; 
      this.selectRandomUsers(); // Llama a la función para seleccionar usuarios
    } catch (error) {
      console.log('Error al obtener los datos de usuario', error);
    }
  },
  methods: {
    //funcion para escoger usuarios al azar 
    selectRandomUsers() {
      if (this.users.length >= 2) { //verifica que el arreglo de objetos se mayor a 2
        const randomIndices = new Set();
        while (randomIndices.size < 2) {
          randomIndices.add(Math.floor(Math.random() * this.users.length));
        }
        this.selectedUsers = Array.from(randomIndices).map(index => {
          return {
            nombre: `${this.users[index].name.first} ${this.users[index].name.last}`,
            imagen: this.users[index].picture.large,
          };
        });
      }
    },
    handleSendMessage(data) {
        // Agregar el mensaje al array messages
        this.messages.push(data);
    },
  },
  computed: {
    datosUsuarios() {
      return this.selectedUsers; 
    },
  },
};
</script>

<template>
  <div class="contenedor">
    <!--le da el primer usuario del arreglo-->
    <formchat v-if="selectedUsers[0]" :user="selectedUsers[0]" @send-message="handleSendMessage"/> 
    <chat :messages="messages" />
    <!--le da el segundo usuario del arreglo-->
    <formchat v-if="selectedUsers[1]" :user="selectedUsers[1]" @send-message="handleSendMessage"/>
  </div>
</template>

<style scoped>
  .contenedor{
    display: flex;
    justify-content: space-evenly;
    width: 100%;
  }
</style>  
