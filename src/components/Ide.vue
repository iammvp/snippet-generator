<template>
    <p class="ide-name">
        {{name}}</p>
</template>

<script>
export default {
    name: 'ide',
    props: {
        name: {
            type: String,
            required: true
        }
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/color.scss';
.ide-name {
    height: 60px;
    line-height: 60px;
    width: 140px;
    color: #fff;
    font-size: 18px;
    text-align: center;
    background: #bbb;
    cursor: pointer;
    margin-bottom: 10px;
    &:last-child {
        margin-bottom: 0px;
    }
    &.ide-name--active {
        color: $theme_color;
        background-color: #fff;
    }
}
</style>