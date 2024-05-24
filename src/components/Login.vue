<template>
  <v-sheet width="300" class="mx-auto">

    <v-form ref="form">
      <v-text-field
        v-model="name"
        :counter="10"
        :rules="nameRules"
        label="Usuario"
        required
      ></v-text-field>

      <v-text-field
        v-model="password"
        :rules="passwordRules"
        label="Contraseña"
        type="password"
        required
      ></v-text-field>

      <div class="d-flex flex-column">
        <v-btn
          color="success"
          class="mt-4"
          block
          @click="validate"
        >
          Ingresar
        </v-btn>

        <v-btn
          color="error"
          class="mt-4"
          block
          @click="reset"
        >
          Borrar Datos
        </v-btn>

        <v-btn
          color="warning"
          class="mt-4"
          block
          @click="resetValidation"
        >
          Inicia Sesión con Google
        </v-btn>
      </div>
    </v-form>
  </v-sheet>
</template>
<script>
export default {
  data: () => ({
    name: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 15) || 'Name must be less than 10 characters',
    ],
    select: null,
    password: '',
    passwordRules: [
      v => !!v || 'La contraseña es requerida',
      v => (v && v.length >= 8) || 'La contraseña debe tener al menos 8 caracteres',
      v => /[A-Z]/.test(v) || 'La contraseña debe tener al menos una letra mayúscula',
      v => /[a-z]/.test(v) || 'La contraseña debe tener al menos una letra minúscula',
      v => /[0-9]/.test(v) || 'La contraseña debe tener al menos un número',
      v => /[\W]/.test(v) || 'La contraseña debe tener al menos un carácter especial (como @, #, $, etc.)'
    ],
    checkbox: false,
  }),

  methods: {
    async validate () {
      const { valid } = await this.$refs.form.validate()

      if (valid) alert('Form is valid')
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    },
  },
}
</script>
<style scoped>

</style>
