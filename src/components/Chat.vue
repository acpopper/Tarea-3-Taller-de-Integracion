<template>
    <form id="form" @submit.prevent="onSubmit">
        <input id="input" autocomplete="off" v-model="message" name="message" />
        <button type="submit" class="btn">Send</button>
    </form>
    
</template>

<script>
export default {
    name: 'Chat',
    data() {
        return{
            message: ''
        }
    },
    methods: {
        onSubmit() {
            this.$emit('enviar-mensaje', this.message)
            this.message = ''
        }
    }
}
</script>

<style>
    #form { background: rgba(0, 0, 0, 0.15); padding: 0.25rem; display: flex; height: 3rem; box-sizing: border-box; backdrop-filter: blur(10px); position: absolute; bottom: 0; right: 0; width: 100%;}
    #input { border: none; padding: 0 1rem; flex-grow: 1; border-radius: 2rem; margin: 0.25rem; }
    #input:focus { outline: none; }
    #form > button { background: #333; border: none; padding: 0 1rem; margin: 0.25rem; border-radius: 3px; outline: none; color: #fff; }

    #messages { list-style-type: none; margin: 0; padding: 0; }
    #messages > li { padding: 0.5rem 1rem; }
    #messages > li:nth-child(odd) { background: #efefef; }
</style>