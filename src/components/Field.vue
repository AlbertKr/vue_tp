<template>
  <component v-bind:is="component"></component>
</template>

<script>
export default {
    name: "Field",
    props: {
        component: Object
    }
}
</script>

<style>

</style>