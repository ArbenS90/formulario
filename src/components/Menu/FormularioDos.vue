<template>
  <div>
    <div class="mb-4">
      <label for="email" class="block text-gray-700 font-bold mb-2">Correo electrónico</label>
      <input type="email" name="email" id="email" v-model="email" :class="{ 'border-red-500': emailError }"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        @input="onChange">
      <p v-if="emailError" class="text-red-500 text-xs italic">Ingresa un correo electrónico válido.</p>
    </div>
    <div class="mb-4">
      <label for="password" class="block text-gray-700 font-bold mb-2">Contraseña</label>
      <input type="password" name="password" id="password" v-model="password" :class="{ 'border-red-500': passwordError }"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      <p v-if="passwordError" class="text-red-500 text-xs italic">La contraseña es obligatoria.</p>
    </div>
    <div class="mb-4">
      <label for="password_confirm" class="block text-gray-700 font-bold mb-2">Confirmación de contraseña</label>
      <input type="password" name="password_confirm" id="password_confirm" v-model="passwordConfirm"
        :class="{ 'border-red-500': passwordConfirmError }"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      <p v-if="passwordConfirmError" class="text-red-500 text-xs italic">Las contraseñas no coinciden.</p>
    </div>
    <div class="mb-4">
      <label for="phone" class="block text-gray-700 font-bold mb-2">Número de teléfono</label>
      <input type="tel" name="phone" id="phone" v-model="phone" :class="{ 'border-red-500': phoneError }"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      <p v-if="phoneError" class="text-red-500 text-xs italic">Ingresa un número de teléfono válido.</p>
    </div>
    <div class="mb-4">
      <label for="cellphone" class="block text-gray-700 font-bold mb-2">Número de celular</label>
      <input type="tel" name="cellphone" id="cellphone" v-model="cellphone" :class="{ 'border-red-500': cellphoneError }"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
      <p v-if="cellphoneError" class="text-red-500 text-xs italic">Ingresa un número de celular válido.</p>
    </div>
    <button type="submit"
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">Enviar</button>

  </div>
</template>

<script>
export default {
  name: 'FormularioDos',
  props: {
    validador: {
      email: String,
      password: String,
      password_confirm: String,
      phone: Number,
      cellphone: Number,
    }
  },
  emits: ['validador', {

  }],
  methods: {
    onChange(e) {
      this.$emit('validador', {
        label: 'FormularioDos',
        data: {
          ...this.validador,
          [e.target.name]: e.target.value
        }
      })
    },
  }
}
</script>