<template>
  <div>
    <h1>Base de Datos con Firebase</h1>
    <div class="form-container">
        <form @submit.prevent="submitUsuario">
            <input v-model="nuevoNombre" placeholder="Ingresa tu nombre" class="input-field" />
            <input v-model="nuevoEmail" placeholder="Ingresa tu email" class="input-field" />
            <input v-model="nuevoTelefono" placeholder="Ingresa tu teléfono" class="input-field" />
            <button type="submit" class="btn-submit">Agregar</button>
        </form>
    </div>
</div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
    data() {
        return {
            nuevoNombre: '',
            nuevoEmail: '',
            nuevoTelefono: ''
        };
    },
    methods: {
        ...mapActions(['addUsuario']),
        async submitUsuario() {
            if (this.nuevoNombre.trim() !== '' && this.nuevoEmail.trim() !== '' && this.nuevoTelefono.trim() !== '') {
                const nuevoUsuario = {
                    nombre: this.nuevoNombre,
                    email: this.nuevoEmail,
                    telefono: this.nuevoTelefono,
                }
                await this.addUsuario(nuevoUsuario); // Llama a la acción de Vuex
                this.nuevoNombre = '';
                this.nuevoEmail = '';
                this.nuevoTelefono = '';
            }
        }
    }
};
</script>
