<template>
    <div class="main">
        <div class="main__left">
            <div class="main__left-top">
                <input-component placeholder="description" @getInputValue="set_description"></input-component>
                <div class="main__left-top__gap"></div>
                <input-component placeholder="prefix" @getInputValue="set_prefix"></input-component>
            </div>
            <div class="main__left-bot">
                <textarea class="main__left-bot-input" placeholder="your code" v-model="code"></textarea>
            </div>
        </div>
        <div class="main__right">
            <div class="main__right-snippet">
                <div class="main__right-snippet-code"><pre>{{vscode_snippet}}</pre></div>
            </div>
            <div class="main__right-ide-type">
                <p class="main__right-ide-name" :class="{'main__right-ide-name--active' : ide == selected_ide}" v-for="(ide,index) in ides" :key="index" @click="change_ide(ide)">{{ide}}</p>
            </div>
        </div>
    </div>
</template>

<script>
import InputComponent from './InputComponent'
export default {
    name: 'main',
    components: {
        'input-component': InputComponent,
    },
    data() {
        return {
            ides: ['VSCode', 'Atom', 'Sublime'],
            selected_ide: 'VSCode',
            code: '',
            description:'',
            prefix:'',
        }
    },
    methods: {
        set_description(description){
            this.description = description;
        },
        set_prefix(prefix){
            this.prefix = prefix;
        },
        change_ide(ide) {
            this.selected_ide = ide;
        },
        decode_input() {
            return this.code.split('\n')
        },
        process_vscode_snippet() {
            let input_code = this.decode_input(),
                len = input_code.length,
                snippet = '';
            for (let i = 0; i < len; i++) {
                if (i == len - 1) {
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
"${this.description}": {
"prefix": "${this.prefix}",
"body": [
${this.process_vscode_snippet()}
],
"description": "${this.description}"
}
            `;
        }
    }
}

</script>

<style lang="scss" scoped>
@import '../style/color.scss';
.main {
    flex: 1;
    padding: 0 20px 20px 20px;
    display: flex;
    .main__left {
        flex: 0.382;
        margin-right: 5px;
        display: flex;
        flex-direction: column;
        .main__left-top {
            padding: 5px;
            background-color: #fff;
            margin-bottom: 5px;
            .main__left-top__gap {
                height: 10px;
            }
        }
        .main__left-bot {
            flex: 1;
            padding: 5px;
            background-color: #fff;
            margin-top: 5px;
            display: flex;
            .main__left-bot-input {
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
    }
    .main__right {
        flex: 0.618;
        margin-left: 5px;
        display: flex;
        .main__right-snippet {
            padding: 5px;
            flex: 1;
            background-color: #fff;
            display: flex;
            .main__right-snippet-code {
                flex: 1;
                border: 1px solid $font_color;
            }
        }

        .main__right-ide-type {
            .main__right-ide-name {
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
                &.main__right-ide-name--active {
                    color: $theme_color;
                    background-color: #fff;
                }
            }
        }
    }
}
</style>
