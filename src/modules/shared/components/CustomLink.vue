<template>
  <a
    v-if="isExternalLink"
    class="normal-link"
    :href="link.to"
    target="_blank"
    >{{ link.name }}</a
  >

  <router-link v-else :to="route" v-slot="{ isActive }">
    <a :class="isActive ? 'is-active' : 'normal-link'">{{
      link.name
    }}</a>
  </router-link>
</template>

<script>
export default {
  props: {
    link: {
      type: Object,
      required: true,
    },
  },
  computed: {
    isExternalLink() {
      return this.link.to.startsWith("http");
    },
    route() {
      return this.link.id == undefined
      ? { name: this.link.to }
      : { name: this.link.to, params: { id: this.link.id } }
    }
  },
};
</script>

<style scoped>
.is-active {
  color: rgb(55, 184, 32);
}

.normal-link {
  color: darkgray;
}
</style>