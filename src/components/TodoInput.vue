<script>
export default {
    data() {
        return {
            todo: ''
        }
    },
    methods: {
        addTodo() {
            if (this.todo.length) {
                const todo = {
                    id: Math.random(),
                    text: this.todo,
                    isChecked: false
                }
                this.$emit('addTodo', todo);
                this.todo = '';
            }
        }
    }
}
</script>

<template>
    <div class="container">

        <form @submit.prevent>
            <div class="input-box">
                <span class="round"></span>
                <input
                  class="input"
                  type="text"
                  placeholder="Create a new todo..."
                  spellcheck="false"
                  v-model="todo"
                  @keypress.enter="addTodo"
                >
            </div>
        </form>

    </div>
</template>

<style lang="scss" scoped>
@import '../main.scss';

.input-box {
    position: relative;
}

.input {
    width: 100%;
    padding: 25px 0;
    margin-bottom: 25px;
    border: none;
    outline: none;
    border-radius: 5px;
    background: $clr-dk-bg-200;
    padding-left: 70px;
    color: $clr-dk-accent-100;
    caret-color: $clr-primary-500;
    box-shadow: $shadow;

    &::placeholder {
        color: $clr-dk-neutral-200;
    }

    @include media-sm {
        font-size: $fs-sm;
    }
}

.round {
    content: '';
    position: absolute;
    top: 50%;
    transform: translateY(-100%);
    left: 22px;
    width: 22px;
    height: 22px;
    border-radius: 50%;
    border: 1px solid $clr-dk-neutral-100;
    pointer-events: none;
}

// light theme
main.light {
    .round {
        border-color: $clr-lt-neutral-300;
    }
    .input {
        background: $clr-lt-bg-200;
        color: $clr-lt-primary-500;
    
        &::placeholder {
            color: $clr-lt-primary-400;
            transition: $ts-200;
        }
    }
}

</style>