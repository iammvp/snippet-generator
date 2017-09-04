<template>
    <div class="input">
        <input class="input-component" type="text" :placeholder="placeholder">
    </div>
</template>

<script>
export default {
    name: 'input-component',
    props: {
        placeholder: {
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
.input {
    width: 100%;
    display: flex;
    .input-component {
        flex: 1;
        border: 1px solid $font_color;
        border-radius: 5px;
        padding: 0 20px;
        height: 60px;
        width: 100%;
        font-size: 18px;
        color: $font_color;
        font-family: inherit;
        &:hover,
        &:focus {
            border: 1px solid $theme_color;
        }
    }
    ::-webkit-input-placeholder {
        color: $font_color;
        font-family: 'Source Code Pro', Consolas, monaco, monospace;
    }
}
</style>
