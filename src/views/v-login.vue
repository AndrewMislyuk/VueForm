<template>
  <div>
    <headerLogo />
    <formLogin />
  </div>
</template>

<script>
import headerLogo from "@/components/v-header.vue";
import formLogin from "@/components/v-form.vue";

export default {
  name: "login",
  components: {
    headerLogo,
    formLogin,
  },
};
</script>

<style lang="scss"></style>
