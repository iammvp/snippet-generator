<template>
    <div class="ide-type">
        <ide name="VSCode"></ide>
        <ide name="Atom"></ide>
        <ide name="Sublime"></ide>
    </div>
</template>

<script>
import Ide from './Ide.vue';
export default {
    name: 'ide-type',
    components: {
        'ide': Ide
    },
    data () {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>

</style>
