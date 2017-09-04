<template>
    <div class="main-right">
        <snippet></snippet>
        <ide-type></ide-type>
    </div>
</template>

<script>
import IdeType from './IdeType';
import Snippet from './Snippet'
export default {
    name: 'main-right',
    components: {
        'ide-type': IdeType,
        'snippet': Snippet,
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
.main-right {
    flex: 0.618;
    margin-left: 5px;
    display: flex;
}
</style>
