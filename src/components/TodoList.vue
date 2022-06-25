<template>
    <div class="screen">
        <div class="todo">
            <input type="text" class="add">
        </div>
        <div>
            <div class="item" v-for="todo in todos">
                {{ todo.text }}
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    data() {
        return {
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
        width: 350px;
        border-radius: 5px;
        border: none;
        height: 25px;
        text-align: center;
        background-color: #3F3F3F;
        color: #fff;
    }
}
</style>