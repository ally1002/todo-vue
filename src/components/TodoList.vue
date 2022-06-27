<template>
    <div class="screen">
        <div class="todo">
            <input type="text" class="add" v-model="newTodo" @keyup.enter="insertTask" placeholder="Write a task">
        </div>
        <div class="list">
            <div class="item" v-for="(todo, index) in todos">
                <button class="btn-done" @click="doneItem(todo)" v-bind:class="{ done: todo.done }" v-if="!todo.edit">
                    {{ todo.text }}
                </button>
                <input type="text" v-else v-model="editingText" @keyup.enter="doneEdit(todo)">
                <button class="icon-right" @click="removeItem(index)">
                    <fas icon="trash"></fas>
                </button>
                <button class="icon-right" @click="editItem(todo)">
                    <fas icon="pencil"></fas>
                </button>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";


export default defineComponent({
    name: 'todo-list',
    data() {
        return {
            newTodo: <string>'',
            idNewTodo: <number>4,
            beforeEdit: '',
            editingText: '',
            todos: [
                {
                    id: 1,
                    text: "Learn Vue",
                    done: false,
                    edit: false
                },
                {
                    id: 2,
                    text: "Learn TypeScript",
                    done: false,
                    edit: false
                },
                {
                    id: 3,
                    text: "Learn Vuex",
                    done: false,
                    edit: false
                }
            ]
        }
    },
    methods: {
        insertTask() {
            if (this.newTodo.trim() === '') {
                return
            }

            this.todos.push({
                id: <number>this.idNewTodo,
                text: <string>this.newTodo,
                done: <boolean>false,
                edit: <boolean>false
            });

            this.idNewTodo++
            this.newTodo = '';
        },
        removeItem(index: number) {
            this.todos.splice(index, 1);
        },
        doneItem(todo: any) {
            todo.done = todo.done === true ? false : true;
        },
        editItem(todo: any) {
            todo.edit = todo.edit === true ? false : true
        },
        doneEdit(todo: any) {
            this.beforeEdit = todo.text;
            if ( this.editingText.trim() == '') {
                this.editingText = this.beforeEdit;
            }

            todo.text = this.editingText;
            todo.edit = false;
        }
    }
});
</script>

<style lang="scss" scoped>
#screen {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;

    font-weight: normal;
}

.todo {
    display: flex;
    justify-content: center;

    .add {
        transition: ease-in-out 0.2s;
        width: 100%;
        font-size: 20px;
        border-radius: 5px;
        border: none;
        height: 40px;
        text-align: center;
        background-color: #3F3F3F;
        color: #fff;
    }
}

.list {
    display: flex;
    flex-direction: column;
    margin-top: 20px;

    .item {
        padding: 5px;

        &:hover {
            border: #41B883;
            border-style: solid;
            border-radius: 5px;
        }

        .btn-done {
            background: none;
            border: none;
            color: var(--color-text);
            font-size: 15px;
            cursor: pointer;

            &:hover {
                color: white;
                transition: 0.2s;
            }
        }

        .done {
            text-decoration: line-through 2px;
            color: #808080;
        }

        .icon-right {
            color: var(--color-text);
            background: none;
            border: none;
            float: right;
            padding: 5px;
            cursor: pointer;

            &:hover {
                color: white;
                transition: 0.2s;
            }
        }
    }
}
</style>