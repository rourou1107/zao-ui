<template>
    <div class="topnav" :class="{background: toggleMenuButtonVisible }">
        <router-link class="logo" to="/">
            <svg class="icon">
                <use xlink:href="#icon-logo"></use>
            </svg>
        </router-link>
        <ul class="menu">
            <li>
                <router-link to="/doc">文档</router-link>
            </li>
        </ul>
        <svg class="icon toggleAside" @click="toggleAside" v-if="toggleMenuButtonVisible">
            <use xlink:href="#icon-mulu"></use>
        </svg>
    </div>
</template>
<script lang="ts">
    import { inject, Ref } from 'vue'
    export default {
        props: {
            toggleMenuButtonVisible: { // 只有文档页需要
                type: Boolean,
                default: false
            }
        },
        setup() {
            const asideVisible = inject<Ref<boolean>>('asideVisible')
            const toggleAside = () => {
                asideVisible.value = !asideVisible.value
            }
            return { toggleAside }
        }
    }
</script>
<style lang="scss" scoped>
    $color: #007974;
    .topnav {
        color: $color;
        display: flex;
        padding: 16px;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 10;
        > .logo {
            max-width: 6em;
            margin-right: auto;
            > svg {
                width: 32px;
                height: 32px;
            }
        }
        > .menu {
            display: flex;
            white-space: nowrap;
            flex-wrap: nowrap;
            > li {
                margin: 0 1em;
                a:hover {
                    text-decoration: none;
                }
            }
        }
        > .toggleAside {
            width: 40px;
            height: 40px;
            position: absolute;
            left: 16px;
            top: 50%;
            transform: translateY(-50%);
            display: none;
        }
        @media (max-width: 500px) {
            > .menu{display: none;}
            > .logo{margin: 0 auto;}
            > .toggleAside {display: inline-block;}
            &.background {
                background: #fbf7f7;
            }
        }
    }
</style>
