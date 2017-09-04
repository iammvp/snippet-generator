<template>
    <div id="app">
        <app-header></app-header>
        <app-main></app-main>
        <!-- <textarea cols="30" rows="10" v-model="code"></textarea>
        <textarea cols="30" rows="10" v-model="vscode_snippet"></textarea> -->
                      
    </div>
</template>

<script>
import Header from './components/Header';
import Main from './components/Main';
export default {
    name: 'app',
    data() {
        return {
            code: ''
        }
    },
    components:{
        'app-header':Header,
        'app-main':Main,
    },
    methods: {
        decode_input() {
            return this.code.split('\n')
        },
        process_vscode_snippet() {
            let input_code = this.decode_input(),
            len = input_code.length,
                snippet = '';
            for (let i = 0; i < len; i++) {
                if (i == len-1) {
                    snippet += `"${input_code[i]}"`;
                } else {
                    snippet += `"${input_code[i]}",\n`;
                }
            }
            return snippet;
        },
    },
    computed: {
        vscode_snippet() {
            this.decode_input();
            return `
"": {
"prefix": "",
"body": [
${this.process_vscode_snippet()}
],
"description": "test"
}
            `;
        }
    }
}
</script>

<style lang="scss" scoped>
    @import './style/color.scss';
    #app{
        width: 100%;
        height: 100%;
        background-color: $theme_color;
        display: flex;
        flex-direction: column;
    }
</style>
