<template>
    <div class="main-left-top">
        <input-component placeholder="description"></input-component>
        <div class="main-left-top__gap"></div>
        <input-component placeholder="prefix"></input-component>
    </div>
</template>

<script>
import InputComponent from './InputComponent'
export default {
    name: 'main-left-top',
    components: {
        'input-component': InputComponent,
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
.main-left-top {
    padding: 5px;
    background-color: #fff;
    margin-bottom: 5px;
    .main-left-top__gap{
        height: 10px;
    }
}
</style>
