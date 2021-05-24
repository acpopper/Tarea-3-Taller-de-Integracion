<template>
    <form @submit.prevent="onSubmit" style="display: inline-block;">
    <label for="fname">Name: </label>
    <input type="text" id="fname" name="name" v-model="nombre">
    <button type="submit" class="btn">Chat</button>
    </form>
</template>

<script>
export default {
    name: 'Name',
    data() {
        return{
            nombre: ''
        }
    },
    methods: {
        onSubmit() {
            this.$emit('name-login', this.nombre)
        }
    }
}
</script>
