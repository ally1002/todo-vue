<template>
    <div class="screen">
        <div class="todo">
            <input type="text" class="add" v-model="newTodo" @keyup.enter="insertTask">
        </div>
        <div class="list">
            <div class="item" v-for="todo in todos">
                {{ todo.text }}
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
            todos: [
                {
                    id: 1,
                    text: "Learn Vue",
                    done: false
                },
                {
                    id: 2,
                    text: "Learn TypeScript",
                    done: false
                },
                {
                    id: 3,
                    text: "Learn Vuex",
                    done: false
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
                done: <boolean>false
            });

            this.idNewTodo++
            this.newTodo = '';
        },
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

        .remove {
            color: var(--color-text);
            background: none;
            border: none;
            cursor: pointer;

            &:hover {
                color: white;
                transition: 0.2s;
            }
        }
    }
}
</style>