<template>
    <div id="app">
        <app-header></app-header>
        <app-main></app-main>
    </div>
</template>

<script>
import Header from './components/Header';
import Main from './components/Main';
export default {
    name: 'app',
    data() {
        return {
        }
    },
    components: {
        'app-header': Header,
        'app-main': Main,
    },
}
</script>

<style lang="scss">
@import './style/color.scss';


#app {
    width: 100%;
    height: 100%;
    background-color: $theme_color;
    display: flex;
    flex-direction: column;
}
</style>
