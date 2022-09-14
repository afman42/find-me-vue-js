<script lang="ts">
import FindMe from './components/FindMe.vue';
import { defineComponent } from 'vue'
export default defineComponent({
    name:"AppVue",
    components: {
        FindMe
    },
})
</script>

<template>
    <div class="container">
        <h1>Find Me</h1>
        <FindMe />
    </div>
</template>
