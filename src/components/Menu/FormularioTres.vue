<template>
    <form>
      <div class="mb-4">
        <label for="address" class="block text-gray-700 font-bold mb-2">Dirección de residencia</label>
        <input type="text" name="address" id="address" v-model="address"
               :class="{ 'border-red-500': addressError }"
               class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
               >
        <p v-if="addressError" class="text-red-500 text-xs italic">Ingresa una dirección válida.</p>
      </div>
      <div class="mb-4">
        <label for="postal_code" class="block text-gray-700 font-bold mb-2">Código Postal</label>
        <input type="text" name="postal_code" id="postal_code" v-model="postalCode"
               :class="{ 'border-red-500': postalCodeError }"
               class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
               >
        <p v-if="postalCodeError" class="text-red-500 text-xs italic">Ingresa un código postal válido.</p>
      </div>
      <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">Enviar</button>
    </form>
  </template>

<script>
export default {
    name: 'FormularioTres',
    props: {
    validador: {
      address: String,
      postal_code: String,
    }
  },
  emits: ['validador', {

  }],
  methods: {
    onChange(e) {
      this.$emit('validador', {
        label: 'FormularioTres',
        data: {
          ...this.validador,
          [e.target.name]: e.target.value
        }
      })
    },
  }
}
</script>