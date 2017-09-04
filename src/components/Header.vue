<template>
    <div class="header">
        <p class="header__title">snippet generator</p>
    </div>
</template>

<script>
export default {
    name: 'header',
    data () {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
    @import '../style/color.scss';
    .header{
        padding: 30px 0 70px 0;
        .header__title{
            text-align: center;
            font-size: 28px;
            color: $font_color;
        }
    }
</style>
