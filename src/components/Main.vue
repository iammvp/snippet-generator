<template>
    <div class="main">
        <div class="main__left">
            <div class="main__left-top">
                <input-component placeholder="description" @setInputValue="set_description"></input-component>
                <div class="main__left-top__gap"></div>
                <input-component placeholder="prefix" @setInputValue="set_prefix"></input-component>
            </div>
            <div class="main__left-bot">
                <textarea class="main__left-bot-input" placeholder="your code" v-model="code"></textarea>
            </div>
        </div>
        <div class="main__right">
            <div class="main__right-snippet">
                <textarea class="main__right-snippet-output" @dblclick.stop.prevent="copy_snippet" v-model="active_snippet" readonly></textarea>
                <p class="main__right-copy-tips">double click to copy your snippet!</p>
            </div>
        </div>
        <div class="main__ide-type">
            <p class="main__ide-name" :class="{'main__ide-name--active' : ide == selected_ide}" v-for="(ide,index) in ides" :key="index" @click="change_ide(ide)">{{ide}}</p>
        </div>
        <p class="copy-notification" :class="{'copy-notification-animation' : is_show_notification == true}">copied!</p>
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
            description: '',
            prefix: '',
            is_show_notification: false,
        }
    },
    methods: {
        set_description(description) {
            this.description = description;
        },
        set_prefix(prefix) {
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
                    snippet += `    "${input_code[i]}"`;
                } else {
                    snippet += `    "${input_code[i]}",\n`;
                }
            }
            return snippet;
        },
        process_atom_snippet() {
            let input_code = this.decode_input(),
                snippet = '';
            input_code.map(c => {
                snippet += `    ${c}\n`;
            });
            return snippet;
        },
        copy_snippet(e) {
            if (this.is_show_notification == false) {
                if (document.selection) {
                    var range = document.body.createTextRange();
                    range.moveToElementText(e.target);
                    range.select();
                } else if (window.getSelection) {
                    var range = document.createRange();
                    range.selectNode(e.target);
                    window.getSelection().removeAllRanges();
                    window.getSelection().addRange(range);
                }
                document.execCommand("copy");
                this.is_show_notification = true;
                setTimeout(() => {
                    this.is_show_notification = false;
                }, 1500);
            }
        }
    },
    computed: {
        vscode_snippet() {
            return `"${this.description}": {\n  "prefix": "${this.prefix}",\n  "body": [\n${this.process_vscode_snippet()}\n  ],\n  "description": "${this.description}"\n}`;
        },
        atom_snippet() {
            return `'${this.description}':\n  'prefix': '${this.prefix}'\n  'body':"""\n${this.process_atom_snippet()}\n  """`
        },
        sublime_snippet() {
            return `<snippet>\n  <content><![CDATA[\n${this.code}\n  ]]></content >\n  <description>${this.description}</description>\n  <tabTrigger><${this.prefix}/tabTrigger>\n  <!-- Optional: Set a scope to limit where the snippet will trigger -->\n  <!-- <scope >source.python</scope > -->\n</snippet >`;
        },
        active_snippet() {
            if (this.selected_ide == 'VSCode') {
                return this.vscode_snippet;
            } else if (this.selected_ide == 'Atom') {
                return this.atom_snippet;
            } else if (this.selected_ide == "Sublime") {
                return this.sublime_snippet;
            }
        }
    }
}

</script>

<style lang="scss">
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
            position: relative;
            .main__right-copy-tips {
                position: absolute;
                top: 20px;
                right: 20px;
            }
            .main__right-snippet-output {
                resize: none;
                border: 1px solid $font_color;
                border-radius: 5px;
                padding: 20px;
                flex: 1;
                font-size: 18px;
                font-family: inherit;
            }
        }
    }
    .main__ide-type {
        .main__ide-name {
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
            &.main__ide-name--active {
                color: $theme_color;
                background-color: #fff;
            }
        }
    }
    .copy-notification {
        position: fixed;
        top: 0;
        right: 0;
        color: $theme_color;
        font-size: 16px;
        height: 60px;
        line-height: 60px;
        background-color: #fff;
        width: 130px;
        text-align: center;
        transform: translateX(100%);
    }
    .copy-notification-animation {
        animation: notification 1.5s;
        @keyframes notification {
            0% {
                transform: translateX(100%);
            }
            25% {
                transform: translateX(0);
            }
            50% {
                transform: translateX(0);
            }
            100% {
                transform: translateX(100%);
            }
        }
    }
}
</style>
