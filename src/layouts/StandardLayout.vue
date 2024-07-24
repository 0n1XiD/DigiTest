<template>
    <div>
        <div class="wrapper">
            <header-view />
            <slot></slot>
        </div>
    </div>
</template>
  
<script>
import HeaderView from '@/components/layout/HeaderView.vue';

export default {
    components: {
      HeaderView
    },
    data() {
      return {

      }
    },
};
</script>

<style lang="scss">
@import "@/assets/css/style.scss";

/* App */
#app{
  overflow-x: hidden;
}

.wrapper {
  overflow: hidden;
  padding: 12px 100px 36px 100px;
  height: 100%;
  background: none;
}

@media (max-width: 992px) {
  .wrapper {
    padding: 12px 50px 36px 50px;
  }
}

@media (max-width: 576px) {
  .wrapper {
    padding: 12px 16px 36px 16px;
  }
}

</style>