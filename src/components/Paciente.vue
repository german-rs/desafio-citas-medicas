<script>
    export default{
        name: 'Paciente',
        props:['nombre', 'fecha', 'hora', 'gravedad', 'motivo']
    }
</script>
<template>
    <div class="ficha_paciente" :aria-labelledby="'ficha-' + nombre">
        <h3>Paciente</h3>
        <p>{{ nombre }}</p>
        <h3>Fecha</h3>
        <p>{{ fecha }}</p>
        <h3>Hora</h3>
        <p>{{ hora }}</p>
        <h3>Motivo</h3>
        <p>{{ motivo }}</p>
        <button
            @click="$emit('eliminar', nombre)"
            >Eliminar</button>
    </div>
</template>

<style scoped>
    .ficha_paciente{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 0.5em;   
    }
</style>