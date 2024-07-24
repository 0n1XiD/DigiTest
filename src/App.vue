<template>
    <div id="app">
        <standard-layout>
            <router-view/>
        </standard-layout>
    </div>
</template>

<script>
import StandardLayout from './layouts/StandardLayout.vue';

export default {
  name: "App",
  components: {
    StandardLayout
  }
};
</script>

<style lang="scss" scoped></style>
