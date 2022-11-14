<template>
    <li class="item">
        <template v-if="!isEdit">
            <input class="form-check-input" type="checkbox" v-model="isCompleteLocal" @change="check">
            <label class="form-check-label" @click="edit" :class="{done: isCompleteLocal}">
                {{ text }}
            </label>
            <button class="btn btn-danger" style="margin-left: auto" @click="$emit('remove', id)">Удалить</button>
        </template>
        <template v-else>
            <input class="form-check-input" type="checkbox" v-model="isCompleteLocal" disabled>
            <input class="form-control" type="text" v-model="newText">
            <button class="btn btn-primary" @click="save">Сохранить</button>
        </template>
    </li>
</template>

<script>
export default {
    emits: ['remove', 'change', 'markComplete'],
    props: {
        id: Number,
        text: String,
        isComplete: Boolean
    },
    data() {
        return {
            isEdit: false,
            newText: this.text,
            isCompleteLocal: this.isComplete,
        }
    },
    methods: {
        edit() {
            this.isEdit = true;

        },
        save() {
            this.isEdit = false;
            this.$emit('change', this.id, this.newText);
        },
        check() {
            this.$emit('markComplete', this.id, this.isCompleteLocal);
        }
    }
}
</script>

<style>
.item {
    display: flex;
    justify-content: left;
    align-items: center;
    max-width: 50%;
    margin: 0 auto;
    padding: 5px 0;
    text-align: left;
}
.item [type='checkbox'] {
    margin-right: 10px;
}
.item label {
    margin-right: 10px;
}
.done {
    text-decoration: line-through;
}
</style>