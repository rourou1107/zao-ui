<template>
    <div>
        <div class="layout">
            <Topnav class="nav" toggleMenuButtonVisible />
            <div class="content">
                <aside v-if="asideVisible">
                    <h2>文档</h2>
                    <ul>
                        <li><router-link to="/doc/intro">介绍</router-link></li>
                        <li><router-link to="/doc/install">安装</router-link></li>
                        <li><router-link to="/doc/get-started">开始使用</router-link></li>
                    </ul>
                    <h2>组件列表</h2>
                    <ul>
                        <li><router-link to="/doc/switch" class="my-a">Switch 组件</router-link></li>
                        <li><router-link to="/doc/button">Button 组件</router-link></li>
                        <li><router-link to="/doc/dialog">Dialog 组件</router-link></li>
                        <li><router-link to="/doc/tabs">Tabs 组件</router-link></li>
                    </ul>
                </aside>
                <main>
                    <router-view />
                </main>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
    import Topnav from '../components/Topnav.vue'
    import { inject, Ref } from 'vue';
    export default {
        components: { Topnav },
        setup() {
            const asideVisible = inject<Ref<boolean>>('asideVisible')
            return { asideVisible }
        }
    }
</script>
<style lang="scss" scoped>
    .layout {
        display: flex;
        flex-direction: column;
        height: 100vh;
        > .nav {
            flex-shrink: 0;
        }
        > .content {
            flex-grow: 1;
            padding-top: 60px;
            padding-left: 156px;
            @media (max-width: 500px) {
                padding-left: 0;
            }
            display: flex;
            > aside {
                flex-shrink: 0;
            }
            > main {
                flex-grow: 1;
                padding: 16px 40px;
                overflow: auto;

            }
            aside {
                background: lightblue;
                width: 150px;
                position: fixed;
                top: 0;
                left: 0;
                padding-top: 70px;
                height: 100%;
                z-index: 2;
                > h2 {
                    margin-bottom: 4px;
                    padding: 0 16px;
                }
                > ul {
                    > li {
                        text-decoration: underline white;
                        a {
                            width: 100%;
                            padding: 4px 16px;
                            text-decoration: none;
                            display: inline-block;
                        }
                        .router-link-active {
                            background: #ffffff;
                        }
                    }
                }
            }
        }
    }
</style>
