<template>
    <CheckItemForm @add="add" />

    <ul v-if="items.length > 0">
        <CheckItem
            v-for="item in items"
            :key="item.id"
            :id=item.id
            :text=item.text
            :isComplete=item.isComplete
            @remove="remove"
            @change="change"
            @markComplete="markComplete"
        />
    </ul>
    <p v-else>Нет записей</p>
</template>

<script>
import CheckItem from './components/CheckItem.vue'
import CheckItemForm from './components/CheckItemForm.vue'

export default {
    name: 'App',
    components: {
        CheckItem,
        CheckItemForm
    },
    data() {
        return {
            items: localStorage.getItem('vueTodoList') ? JSON.parse(localStorage.getItem('vueTodoList')) : [],
        }
    },
    methods: {
        remove(id) {
            this.items = this.items.filter((item) => {
                return item.id !== id;
            })
            localStorage.setItem('vueTodoList', JSON.stringify(this.items))
        },
        change(id, text) {
            this.items = this.items.map((item) => {
                if (item.id === id) {
                    item.text = text;
                }
                return item;
            });
            localStorage.setItem('vueTodoList', JSON.stringify(this.items))
        },
        add(text) {
            let id = this.items.length + 1;

            this.items.push({
                id: id,
                text: text,
                isComplete: false
            });
            localStorage.setItem('vueTodoList', JSON.stringify(this.items))
        },
        markComplete(id, isComplete) {
            this.items = this.items.map((item) => {
                if (item.id === id) {
                    item.isComplete = isComplete;
                }
                return item;
            });
            console.log(JSON.stringify(this.items))
            localStorage.setItem('vueTodoList', JSON.stringify(this.items))
        }
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
ul {
    padding: 0;
    margin: 0;
}
</style>
