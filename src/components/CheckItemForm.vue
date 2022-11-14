<template>
<form>
    <div class="mb-3">
        <input class="form-control" v-model="newText">

        <button class="btn btn-primary" @click.prevent="save">Добавить</button>
    </div>
</form>
</template>

<script>
export default {
    name: "CheckItemForm",
    emits: ['add'],
    data() {
        return {
            newText: ''
        }
    },
    methods: {
        save() {
            this.$emit('add', this.newText)
            this.newText = ''
        }
    }
}
</script>

<style>
form {
    max-width: 50%;
    margin: 0 auto;
}
</style>