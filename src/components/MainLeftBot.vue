<template>
    <div class="main-left-bot">
        <textarea class="input-code" placeholder="your code"></textarea>
    </div>
</template>

<script>
export default {
    name: 'main-left-bot',
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/color.scss';
.main-left-bot {
    flex: 1;
    padding: 5px;
    background-color: #fff;
    margin-top: 5px;
    display: flex;
    .input-code {
        resize: none;
        border: 1px solid $font_color;
        border-radius: 5px;
        padding: 20px;
        flex: 1;
        font-size: 18px;
        font-family: inherit;
        &:hover,
        &:focus {
            border: 1px solid $theme_color;
        }
    }
}
</style>
