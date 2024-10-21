<script>
    export default{
        props: {
            user: Object // Recibe el objeto del usuario
        },
        data() {
            return {
                newMessage: '',
                color: '',
            };
        },
        methods:{
            sendMessage(){
                if(this.newMessage.trim()){ //verificar si no esta vacio
                    this.$emit('send-message', { //para enviar el mensaje
                        message: this.newMessage,
                        color: this.color,
                        user: this.user
                    });
                    this.newMessage = ''; 
                }
            }
        }
    }
</script>
<template>
    <div class="contenedor-form">
        <div class="contenedor-datos">
            <img :src="user.imagen" alt="Imagen de {{ usuario.nombre }}">
            <h4>{{ user.nombre }}</h4>
        </div>
        <div class="contenedor-input">
            <input v-model="color" type="color"/>
            <textarea v-model="newMessage"/>
            <button @click="sendMessage">Enviar</button>
        </div>
    </div>

</template>
<style scoped>
.contenedor-form {
    display: flex;
    flex-direction: column;
    box-shadow: -1px -1px 6px 0 rgba(128, 128, 128, 0.6), 4px 4px 16px 2px rgba(64, 64, 64, 0.5);
    border-radius: 5px;
  }
  
  .contenedor-datos {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 10px 0;
  }
  
  .contenedor-datos img {
    width: 200px; 
    height: 200px;
    border-radius: 30%; 
    margin-right: 10px;
    box-shadow: -1px -1px 6px 0 rgba(128, 128, 128, 0.6), 4px 4px 16px 2px rgba(64, 64, 64, 0.5);
  }
  
  .contenedor-input {
    display: flex;                
    flex-direction: column;      
    gap: 10px;                   
    background-color: #f9f9f9;  
    padding: 15px;              
    border-radius: 8px;        
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1); 
  }
  
  input[type="color"] {
    width: 100%;                 
    height: 40px;              
    border: none;                
    cursor: pointer;            
  }
  
  textarea {
    width: 90%;                 
    height: 120px;              
    padding: 10px;              
    border: 1px solid #ccc;    
    border-radius: 4px;         
    resize: none;              
    font-size: 16px;            
    line-height: 1.5;           
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1); 
  }
  
  button {
    padding: 10px 15px;         
    background-color: #3EB43C;  /* Color de fondo azul */
    color: white;                /* Color de texto blanco */
    border: none;                /* Sin borde */
    border-radius: 4px;         /* Bordes redondeados */
    cursor: pointer;             /* Cambia el cursor al pasar sobre el botón */
    transition: background-color 0.3s; /* Transición suave para el color de fondo */
  }
  
  button:hover {
    background-color: #7CFF4D;  /* Color de fondo más oscuro al pasar el cursor */
  }
  
</style>