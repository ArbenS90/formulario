<template>
    <div class="">
        Formulario 1

    </div>
    <br>
    <div>
        <label class="font-bold text-lg" for="pais">Selecciona tu pais</label>
        <div class="">
            <select

            class="text-2xl p-2 border-collapse" id="country" v-model="selectedCountry"
            @input="onChange">
                <option disabled value="">Seleccione un país</option>
                <option v-for="country in countries" :key="country.alpha2Code" :value="country.name">{{ country.name }}
                </option>
            </select>
            <div class="">

            </div>
        </div>
    </div>
    <br>
    <div class="">
        <label class="font-bold" for="gender">
            Género
        </label>
        <div class="">
            <select class="" id="gender" name="genero"
            @input="onChange"
            >
                <option disabled>Seleccione una opción</option>
                <option>Masculino</option>
                <option>Femenino</option>
                <option>No binario</option>
            </select>
            <div class="">

            </div>
        </div>
    </div>
    <div class="">
        <label class="" for="firstName"> Primer Nombre </label>
        <input v-bind:value="validador.nombre1" 
        class="" id="firstName" type="text" name="nombre"
        @input="onChange"
        >
    </div>

    <div class="">
        <label class="" for="lastName"> Segundo Nombre </label>
        <input v-bind:value="validador.nombre2"
        class="" id="lastName" type="text" name="nombre2">
    </div>

    <div class="mb-4">
        <label class="" for="birthdate">
            Fecha de nacimiento
        </label>
        <input class="" id="birthdate" type="date" max="{{ maxBirthdate }}" v-model="birthdate" @input="validateAge, onChange"  name="nacimiento">
        <p v-if="ageError" class="text-red-500 text-xs italic">{{ ageError }}</p>
    </div>
    <div class="mb-4">
        <label class="" for="tipo_documento">
            Tipo de Documento
        </label>
        <div class="relative">
            <select v-bind:value="validador.tipo_documento"
            class="" id="tipo_documento" name="tipo_documento" v-model="selectedTipoDocumento"
            @input="onChange"
            >
                <option value="" disabled>Seleccione un tipo de documento</option>
                <option value="cc">Cedula de ciudadanía</option>
                <option value="p">Pasaporte</option>
                <option value="ce">Cedula de extranjería</option>
            </select>

        </div>
    </div>


    <div class="mb-4">
        <label for="numero_documento" class="text-sm font-medium text-gray-900">Numero Documento</label>
        <input v-bind:value="validador.numero_documento"
        type="number" id="numero_documento" name="numero_documento" placeholder="Ingrese su número de documento"
            class=""
            @change="uploadfile"
            >
    </div>


    <div class="">
        <label for="foto_frente" class="">Foto Documento - Frente</label>
        <input v-bind:value="validador.foto_frente"
        type="file" id="foto_frente" name="foto_frente" accept=".jpg" class="" @input="onChange"
        >
    </div>


    <div class="divide-y divide-gray-200">

        <label for="foto_reverso" class="block text-gray-700 font-bold mb-2">Foto Documento - Reverso</label>
        <input v-bind:value="validador.foto_reverso"
         type="file" id="foto_reverso" name="foto_reverso" accept=".jpg" class=""
         @change="uploadfile"
         />
    </div>
    <br>
</template>

<script>
export default {
    name: 'FormularioUno',
    props: {
        validador: {
        pais: String,
        genero: String,
        nombre: String,
        nombre2: String,
        nacimiento: String,
        tipo_documento: String,
        numero_documento: Number,
        foto_frente: String,
        foto_reverso: String

        }
    },
    emits: ['validador',{

    }],
    data() {
        return {

            selectedCountry: '',
            countries: [],
            birthdate: null,
            ageError: null,
            maxBirthdate: new Date(new Date().setFullYear(new Date().getFullYear() - 18)).toISOString().split("T")[0],
            selectedTipoDocumento: '',

        };
    },
    async created() {
        try {
            const response = await fetch('https://restcountries.com/v2/all');
            this.countries = await response.json();
        } catch (error) {
            console.error(error);
        }
    },
    methods: {
        uploadfile(e) {
            const file = e.target.files[0];
            if (!file){
                return;
            }

            const fileReader = new FileReader();

            fileReader.onload = () => {

                this.$emit('validador', {
                label: 'FormularioUno',
                data: {
                    ...this.validador,
                    profilePicture: fileReader.result
                }
            })
            }
            fileReader.readAsDataURL(file)
        },
        onChange (e) {
            this.$emit('validador', {
                label: 'FormularioUno',
                data: {
                    ...this.validador,
                    [e.target.name]: e.target.value
                }
            })
        },
        validateAge() {
            if (this.birthdate) {
                const age = new Date().getFullYear() - new Date(this.birthdate).getFullYear();
                if (age < 18) {
                    this.ageError = "Debes tener al menos 18 años";
                } else {
                    this.ageError = null;
                }
            }
        }
    },
}
</script>

<style></style>