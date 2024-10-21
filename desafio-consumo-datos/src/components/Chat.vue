<script>
export default {
    props: {
        messages: Array //arreglo de mensaje (usuario, mensaje y color)
    },
    methods: {
        getBackgroundColor(hexColor) {
            // Convierte el color hexadecimal a RGBA
            const hex = hexColor.replace('#', '');
            const r = parseInt(hex.substring(0, 2), 16);
            const g = parseInt(hex.substring(2, 4), 16);
            const b = parseInt(hex.substring(4, 6), 16);
            const alpha = 0.5;
            return `rgba(${r}, ${g}, ${b}, ${alpha})`;
        }
    }
};
</script>

<template>
    <div class="chat-container">
        <div class="message-container">
            <div v-for="(message, index) in messages" :key="index" class="message" :style="{ backgroundColor: getBackgroundColor(message.color)}" >
                <div class="message-header">
                    <img :src="message.user.imagen" alt="Usuario" class="user-image" />
                    <strong>{{ message.user.nombre }}</strong>
                </div>
                <p class="message-text">{{ message.message }}</p>
            </div>
        </div>
    </div>
</template>
<style scoped>
.chat-container {
    width: 700px;
    border-radius: 5%;
    padding: 10px; 
    box-shadow: -1px -1px 6px 0 rgba(128, 128, 128, 0.6), 4px 4px 16px 2px rgba(64, 64, 64, 0.5);
}
.message-container {
    max-height: 500px; 
    overflow-y: auto; 
    margin: 10px 0; 
}
.message {
    margin-bottom: 10px; 
    margin-left: 15px;
    padding: 10px; 
    border-radius: 15px; 
    width: 90%;
    min-height: 50px;
    height: auto;
}

.message-header {
    display: flex;
    align-items: center;
}

.user-image {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    margin-right: 8px;
}
.message-text {
    margin-top: 5px;
}
</style>
