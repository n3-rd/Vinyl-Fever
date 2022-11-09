<script>
import luge from "@waaark/luge";
export default {
  name: "App",
  mounted() {
    luge.lifecycle.refresh();
  },
};
</script>

<template>
  <RouterView />
</template>
