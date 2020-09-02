<template>
  <div>
    <headerLogo />
    <successModal />
  </div>
</template>

<script>
import headerLogo from "@/components/v-header.vue";
import successModal from "@/components/v-modal.vue";

export default {
  name: "success",
  components: {
    headerLogo,
    successModal,
  },
};
</script>

<style lang="scss"></style>
