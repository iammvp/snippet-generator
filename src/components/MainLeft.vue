<template>
    <div class="main-left">
        <main-left-top></main-left-top>
        <main-left-bot></main-left-bot>
    </div>
</template>

<script>
import MainLeftTop from './MainLeftTop';
import MainLeftBot from './MainLeftBot';
export default {
    name: 'main-left',
    components:{
        'main-left-top':MainLeftTop,
        'main-left-bot':MainLeftBot,
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
.main-left {
    flex: 0.382;
    margin-right: 5px;
    display: flex;
    flex-direction: column;
}
</style>
