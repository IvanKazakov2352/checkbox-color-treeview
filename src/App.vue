<template>
  <div id="app">
    <div class="container">
      <Checkboxes @checkeds="openItem" />
      <CheckboxesItems :items="items" :checkbox="childItem" />
    </div>
  </div>
</template>
<script>
const Checkboxes = () => import("@/components/Checkboxes.vue");
const CheckboxesItems = () => import("@/components/CheckboxItem.vue");
export default {
  data: () => ({
    items: [],
    childItem: {},
  }),
  methods: {
    openItem(data) {
      this.items = data;
    },
  },
  components: {
    Checkboxes,
    CheckboxesItems,
  },
};
</script>
<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  margin-left: 10px;
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}
@media (max-width: 968px) {
  .container {
    flex-direction: column;
    justify-content: center;
  }
}
</style>
