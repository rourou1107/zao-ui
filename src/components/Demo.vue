<template>
    <div class="demo">
        <h2>{{component.__sourceCodeTitle}}</h2>
        <div class="demo-component">
            <Component :is="component" />
        </div>
        <div class="demo-actions">
            <Button @click="toggle">查看代码</Button>
        </div>
        <div class="demo-code" v-if="buttonVisible">
            <pre v-html="Prism.highlight(component.__sourceCode, Prism.languages.html, 'html')" class="language-html" />
        </div>
    </div>
</template>
<script lang="ts">
    import 'prismjs'
    import 'prismjs/themes/prism.css'
    import Button from '../lib/Button.vue';
    import { ref } from 'vue'
    export default {
        components: {Button},
        props: {
            component: {
                type: Object
            }
        },
        setup() {
            const buttonVisible = ref<boolean>(false)
            const Prism = (window as any).Prism
            const toggle = () => {
                buttonVisible.value = !buttonVisible.value
            }
            return { Prism, toggle, buttonVisible }
        }
    }
</script>
<style lang="scss" scoped>
    $border-color: #d9d9d9;
    .demo {
        border: 1px solid $border-color;
        margin: 16px 0 32px;

        > h2 {
            font-size: 20px;
            padding: 8px 16px;
            border-bottom: 1px solid $border-color;
        }

        &-component {
            padding: 16px;
        }

        &-actions {
            padding: 8px 16px;
            border-top: 1px dashed $border-color;
        }

        &-code {
            padding: 8px 16px;
            border-top: 1px dashed $border-color;

            > pre {
                line-height: 1.1;
                font-family: Consolas, 'Courier New', Courier, monospace;
                margin: 0;
            }
        }
    }

</style>
