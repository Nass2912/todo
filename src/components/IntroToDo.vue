<template>
    <div class="mt-3">
        <h1>
            Task Mania App 👋
        </h1>
        <vueTyperNext 
            data="A place to safe keep all your important tasks"
            typeSpeed=35
            handlerNum=1
        />
    </div>
</template>

<script setup>
  import { vueTyperNext } from "vue-typer-next";
</script>

<style scoped>
    div {
        text-align: center;
    }
    .content {
        justify-content: center;
    }
</style>