<template>
    <section class="add-todo">
        <button v-if="!isFormVisable" class="add-todo__show-form-button" @click="openForm">
            <i class="bi bi-plus-lg"></i>
        </button>
        <form v-else class="add-todo__form" @submit.prevent="addTodo">
            <button class="close-button" type="button" @click="closeForm">
                <i class="bi bi-x"></i>
            </button>
            <div class="text-input text-input--focus">
                <input class="input" v-model="todoText"/>
            </div>
            <button class="button button--filled">Add task</button>
        </form>
    </section>
</template>

<script lang="ts">
import { Todo } from '@/types/Todo';
import { defineComponent } from 'vue';

interface State {
    isFormVisable: boolean,
    todoText: string
}

export default defineComponent({
    data(): State {
        return {
            isFormVisable: false,
            todoText:''
        }
    },
    methods: {
        openForm(){
            this.isFormVisable = true
        },
        closeForm() {
            this.isFormVisable = false
        },
        addTodo(){
            this.$emit('addTodo', {
                id: Date.now(),
                text: this.todoText,
                completed: false
            })
            this.todoText = ''
        }
    },
    emits: {
        addTodo: (todo: Todo) => todo
    }
})
</script>