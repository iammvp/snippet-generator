<template>
    <div class="main">
        <main-left></main-left>
        <main-right></main-right>
    </div>
</template>

<script>
import MainLeft from './MainLeft'
import MainRight from './MainRight'
export default {
    name: 'main',
    components:{
        'main-left':MainLeft,
        'main-right':MainRight,
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
.main {
    flex: 1;
    padding: 0 20px 20px 20px;
    display: flex;
}
</style>
