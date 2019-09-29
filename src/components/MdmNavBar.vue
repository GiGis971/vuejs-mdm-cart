<template>
  <div>
    <b-navbar toggleable="md" class="shadow">
      <b-navbar-brand href="/"><MdmLogo /></b-navbar-brand>
      <b-navbar-nav class="ml-auto">
        <b-nav-item href="https://github.com/GiGis971/" target="_blank">
          Github
        </b-nav-item>
        <b-nav-item href="/" disabled>
          Panier <b-badge variant="success">{{ totalCartItems }}</b-badge>
        </b-nav-item>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
import MdmLogo from "./MdmLogo";
export default {
  name: "MdmNavBar",
  components: {
    MdmLogo
  },
  props: {
    totalCartItems: {
      type: Number,
      required: true
    }
  }
};
</script>

<style scoped lang="scss"></style>
