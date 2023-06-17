<script>
</script>

<template>
    <div class="container">

        <header class="header">
            <!-- logo -->
            <a href="/">
                <img src="../assets/logo.png" alt="Logo" class="header__brand">
            </a>
            <!-- theme switch -->
            <button
                @click="$emit('toggleTheme')"
                class="header__theme-switch"
            >
                <img src="../assets/icon-sun.svg" class="sun">
                <img src="../assets/icon-moon.svg" class="moon">
            </button>
        </header>

    </div>
</template>

<style lang="scss" scoped>
@import '../main.scss';

.header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 80px;
    padding-bottom: 50px;

    &__brand {
        width: 160px;
    }

    &__theme-switch {
        position: relative;
        background: none;
        border: none;
        cursor: pointer;

        img {
            position: absolute;
            left: -28px;
            width: 28px;
            transition: $ts-200;

            &.moon {
                opacity: 0;
            }
        }
    }
}

// light theme
main.light {
    .header__theme-switch img {
        &.moon {
            opacity: 1;
        }

        &.sun {
            opacity: 0;
        }
    }
}
</style>