<template>
    <Demo :component="Dialog1Demo"/>
    <Demo :component="Dialog2Demo"/>
</template>
<script lang="ts">
    import Dialog1Demo from './Dialog1.demo.vue'
    import Dialog2Demo from './Dialog2.demo.vue'
    import Demo from './Demo.vue';
    export default {
        components: { Demo },
        setup() {
            return { Dialog1Demo, Dialog2Demo }
        }
    }
</script>
