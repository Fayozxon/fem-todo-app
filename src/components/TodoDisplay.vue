<script>
export default {
    props: ['todos','filter'],
}
</script>

<template>
    <div v-if="todos.length" class="container">
        <section class="todos-box">
            <!-- todos -->
            <ul class="todos-box__todos">
                <li
                  v-for="todo in todos"
                  :class="{checked: todo.isChecked}"
                  @click.self="$emit('checkTodo', todo.id)"
                  :key="todo.id"
                >
                    {{ todo.text }}
                    <button class="deleteBtn" @click.prevent="$emit('deleteTodo', todo.id)">
                        <img src="../assets/icon-cross.svg">
                    </button>
                </li>
            </ul>
            <!-- settings -->
            <div class="todos-box__settings">
                <p class="subtitle">{{ todos.filter(todo => todo.isChecked == false).length }} items left</p>
                <p class="filters">
                    <button @click="$emit('setFilter', 'all')" :class="{active: filter=='all'}">All</button>
                    <button @click="$emit('setFilter', 'active')" :class="{active: filter=='active'}">Active</button>
                    <button @click="$emit('setFilter', 'checked')" :class="{active: filter=='checked'}">Completed</button>
                </p>
                <button @click="$emit('deleteChecked')">Clear completed</button>
            </div>
        </section>
        <!-- info -->
        <p class="info">
            Drag and drop to reoder list
        </p>
    </div>
</template>

<style lang="scss" scoped>
@import '../main.scss';

.todos-box {
    background: $clr-dk-bg-200;
    border-radius: 5px;
    box-shadow: $shadow;

    &__todos {
        position: relative;
        list-style: none;

        li {
            position: relative;
            padding: 20px 25px;
            cursor: pointer;
            border-bottom: 1px solid $clr-dk-primary-300;
            transition: $ts-200;
            user-select: none;
            padding-left: 70px;
            display: flex;
            align-items: center;
            justify-content: space-between;

            @include media-sm {
                font-size: $fs-sm;
            }

            &.checked {
                text-decoration: line-through;
                color: $clr-dk-neutral-200;

                &::after {
                    opacity: 1;
                }
            }

            .deleteBtn {
                cursor: pointer;
                background: none;
                border: none;
                transition: $ts-200;
                opacity: 0;

                @include media-sm {
                    opacity: 1;
                }

                img {
                    width: 16px;
                    filter: brightness(1.5);
                }
            }

            &:hover .deleteBtn {
                opacity: 1;
            }

            &::before {
                content: '';
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
                left: 22px;
                width: 22px;
                height: 22px;
                border: 1px solid $clr-dk-neutral-100;
                border-radius: 50%;
                transition: $ts-200;
            }

            &::after {
                content: url('../assets/icon-check.svg');
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
                left: 22px;
                width: 24px;
                height: 24px;
                background: $gradient-accent;
                // border: 1px solid $clr-dk-neutral-100;
                border-radius: 50%;
                display: flex;
                justify-content: center;
                align-items: center;
                transition: $ts-200;
                opacity: 0;
            }
        }
    }

    &__settings {
        position: relative;
        display: flex;
        justify-content: space-between;
        font-size: $fs-sm;
        padding: 20px 25px;
        color: $clr-dk-neutral-200;

        .filters {
            display: flex;
            gap: 10px;

            @include media-sm {
                position: absolute;
                top: 150%;
                left: 0;
                right: 0;
                box-shadow: $shadow;
                padding: 20px;
                border-radius: 5px;
                justify-content: center;
                background: $clr-dk-bg-200;
                gap: 25px;
            }
        }

        button {
            background: transparent;
            border: none;
            cursor: pointer;
            color: $clr-dk-neutral-200;
            transition: $ts-200;

            &:hover {
                color: $clr-dk-hover-100;
            }

            &.active {
                color: $clr-primary-500;
            }
        }
    }
}

.info {
    padding-top: 50px;
    text-align: center;
    color: $clr-dk-neutral-100;
    font-size: $fs-sm;

    @include media-sm {
        padding-top: 120px;
    }
}

// light theme

main.light {
    .todos-box {
        background: $clr-lt-bg-200;

        &__todos {
            li {
                color: $clr-lt-primary-500;
                border-bottom-color: $clr-lt-neutral-200;

                &.checked {
                    color: $clr-lt-neutral-300;
                }

                &::before {
                    border-color: $clr-lt-neutral-300;
                }
            }
        }

        &__settings {
            .filters {
                @include media-sm {
                    background: $clr-lt-bg-200;
                }
            }

            button {
                color: $clr-lt-primary-400;

                &:hover {
                    color: $clr-lt-primary-500;
                }

                &.active {
                    color: $clr-primary-500;
                }
            }
        }
    }

    .info {
        color: $clr-lt-primary-400;
    }
}

// transitions
// .list-move,
// .list-enter-active,
// .list-leave-active {
//   transition: all 300ms ease-in-out !important;
// }

// .list-enter-from,
// .list-leave-to {
//   opacity: 0;
//   transform: translateX(60px);
// }
// .list-leave-active {
//   position: absolute;
// }
</style>