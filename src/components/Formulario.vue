<script>
    import Paciente from './Paciente.vue';
    export default{
        components:{
            Paciente
        },
        data(){
            return{
                pacientes:[],
                nombre: '',
                fecha: '',
                hora: '',
                gravedad: '',
                motivo: ''
            }
        },
        methods:{
            agregarPaciente(){
                this.pacientes.push({
                    nombre: this.nombre,
                    fecha: this.fecha,
                    hora: this.hora,
                    gravedad: this.gravedad,
                    motivo: this.motivo
                });

                this.limpiarCampos();
            },
            eliminarPaciente(nombre){
                this.pacientes = this.pacientes.filter(
                    paciente => paciente.nombre !== nombre
                );
            },
            limpiarCampos(){
                this.nombre = '',
                this.fecha = '',
                this.hora = '',
                this.gravedad = '',
                this.motivo = ''
            }
        },
        mounted(){
            this.$refs.inputNombre.focus();
        }
    }
</script>
<template>
    <form class="formulario" @submit.prevent="agregarPaciente" aria-labelledby="formulario-header" role="form">
        <div class="formulario__contenedor">
            <div class="formulario__grupo">            
                <div class="formulario__campo">
                    <label
                        :class="{'colorAlerta': nombre == ''}" 
                        for="nombre">Paciente</label>
                    <input v-model="nombre" ref="inputNombre" type="text" name="nombre" id="nombre" aria-required="true" aria-label="Nombre del paciente" aria-describedby="ayuda-nombre">
                    <span id="ayuda-gravedad" class="formulario__ayuda">Introduzca el nombre completo del paciente.</span>
                </div>
                <div class="formulario__campo">
                    <label
                        :class="{'colorAlerta': fecha == ''}"
                        for="fecha">Fecha</label>
                    <input v-model="fecha" type="date" name="fecha" id="fecha" aria-required="true" aria-label="Fecha de consulta" aria-describedby="ayuda-fecha">
                    <span id="ayuda-fecha" class="formulario__ayuda">Seleccione la fecha de consulta.</span>
                </div>
                <div class="formulario__campo">
                    <label
                        :class="{'colorAlerta': hora == ''}" 
                        for="hora">Hora</label>
                    <input v-model="hora" type="time" name="hora" id="hora" aria-required="true" aria-label="Hora de consulta" aria-describedby="ayuda-hora">
                    <span id="ayuda-hora" class="formulario__ayuda">Seleccione la hora de la consulta.</span>
                </div>
                <div class="formulario__campo">
                    <label
                        :class="{'colorAlerta': motivo == ''}" 
                        for="motivo">Motivo</label>
                    <input v-model="motivo" type="text" name="motivo" id="motivo" aria-required="true" aria-label="Motivo de la consulta" aria-describedby="ayuda-motivo" >
                    <span id="ayuda-motivo" class="formulario__ayuda">Especifique el motivo de la consulta.</span>
                </div>
                <div class="formulario__campo">
                    <label 
                        :class="{'colorAlerta': gravedad == ''}"
                        for="gravedad">Gravedad</label>
                    <select v-model="gravedad" name="gravedad" id="gravedad" aria-required="true" aria-label="Nivel de gravedad" aria-describedby="ayuda-gravedad"> 
                        <option value="" disabled selected>Seleccione un nivel</option>
                        <option value="baja">Baja</option>
                        <option value="media">Media</option>
                        <option value="alta">Alta</option>
                    </select>
                    <span id="ayuda-gravedad" class="formulario__ayuda">Seleccione el nivel de gravedad del paciente.</span>
                </div>
            </div>
            <div class="formulario__boton">
                <button
                    :disabled="nombre === '' || fecha === '' || hora === '' || gravedad === '' || motivo === ''"
                    type="submit" aria-label="Agregar paciente">Agregar</button>
            </div>
        </div>
    </form>
    <section class="consultas__registradas" aria-labelledby="consultas-header">
        <div class="mensaje__contenedor">
            <h3 
                v-show="pacientes.length === 0" 
                class="colorAlerta"
            >Aún no hay consultas registradas</h3>
        </div>

        <div class="tarjetas">
            <div 
                :class="{
                    'tarjeta__paciente': true,
                    'fondoGravedadBaja': paciente.gravedad == 'baja',
                    'fondoGravedadMedia': paciente.gravedad == 'media',
                    'fondoGravedadAlta': paciente.gravedad == 'alta'    
                }"
                v-for="paciente in pacientes" 
                role="region" 
                :aria-labelledby="'paciente-' + paciente.nombre"
                aria-live="polite"
                >
                <Paciente
                    :nombre="paciente.nombre"
                    :fecha="paciente.fecha"
                    :hora="paciente.hora"
                    :gravedad="paciente.gravedad"
                    :motivo="paciente.motivo"
                    @eliminar="eliminarPaciente(paciente.nombre)"
                />
            </div>
        </div>
    </section>
</template>

<style scoped>
    .formulario__contenedor{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 1em;
        padding: 1em;
        border: 2px solid var(--clr-gray600);
        border-radius: 10px;
    }

    .formulario__campo{
        border: 2px solid var(--clr-gray600);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 0.5em;
        padding: 1em 0;
        width: 250px;
        height: 130px;
        border-radius: 10px;
    }

    .formulario__grupo{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 0.4em
    }

    .formulario__ayuda{
        text-align: center;
        font-size: 0.8em;
        padding: 0.2em;
    }

    .consultas__registradas{
        margin-top: 1em;
        border: 2px solid var(--clr-gray600);
        width: 100%;
        height: auto;
        padding: 1em;
        border-radius: 10px;
        display: flex;
        flex-direction: column;
    }

    .tarjetas{
        display: flex;
        flex-direction: row;
        gap: 1em;
        flex-wrap: wrap;
    }

    .tarjeta__paciente{
        border: 2px solid var(--clr-gray600);
        border-radius: 10px;
        padding: 2em;
    }

    .colorAlerta{
        color:var(--clr-red500);
    }

    .mensaje__contenedor{
        text-align: center
    }

    .fondoGravedadBaja{
        background-color: var( --clr-green400);
    }
    
    .fondoGravedadMedia{
        background-color: var(--clr-yellow400)
    }

    .fondoGravedadAlta{
        background-color: var(--clr-red400);
    }
</style>