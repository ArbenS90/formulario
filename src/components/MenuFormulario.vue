<template>
    <div class="w-1/2 m-auto">
        <div v-if="!submitted">
            <component v-bind:is="formularios[formularioActual].component"
                v-bind:validador="validador[formularios[formularioActual].label]" @validadorChange="updateValidador" />
            <div class="text">
                <button v-if="formularioActual < formularios.length - 1" v-on:click="next"
                    class="text-center p-5 text-5xl mt-4">
                    siguiente
                </button>
            </div>
            <div class="text">
                <button v-if="formularioActual !== 0" v-on:click="previuos" class="text-center p-5 text-5xl mt-4">
                    Anterior
                </button>
                <button v-else class="text-2xl bg-green-500 text-white p-5 rounded" v-on:click="submit">
                    Enviar
                </button>
                
            </div>
            
            
        </div>
        
        <div v-else class="text-5xl font-bold text-center">
        <span>
            Se han enviado todos los datos con exito!
        </span>
    </div>
    </div>
   
</template>

<script>

import FormularioUno from './Menu/FormularioUno.vue';
import FormularioDos from './Menu/FormularioDos.vue';
import FormularioTres from './Menu/FormularioTres.vue';

export default {
    name: 'MenuFormulario',
    data() {
        return {
            formularioActual: 0,
            submitted: false,
            validador: {
                formularioUno: {
                    pais: '',
                    genero: '',
                    nombre1: '',
                    nombre2: '',
                    nacimiento: '',
                    tipo_documento: '',
                    numero_documento: '',
                    foto_frente: '',
                    foto_reverso: ''
                },
                formularioDos: {
                    email: '',
                    password: '',
                    password_confirm: '',
                    phone: '',
                    cellphone: ''
                },
                formularioTres: {
                    direccion: '',
                    codPostal: ''
                },

            },
            formularios: [
                {
                    component: FormularioUno,
                    label: 'formularioUno'
                },
                {
                    component: FormularioDos,
                    label: 'formularioDos'
                },
                {
                    component: FormularioTres,
                    label: 'formularioTres'
                },
            ]
        }

    },
    methods: {
        next() {
            this.formularioActual += 1;
        },
        previuos() {
            this.formularioActual -= 1;
        },
        updateValidador(payload) {
            this.validador = {
                ...this.validador,
                [payload.label]: payload.data
            }
        },
        submit() {
            this.submitted = true;
            console.log(this.validador)
        }
    },
    components: [
        FormularioUno,
        FormularioDos,
        FormularioTres
    ]
}
</script>