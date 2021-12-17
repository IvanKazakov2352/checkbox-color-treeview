<template>
  <div class="checkboxes-block-items">
    <div class="items">
      <div v-for="item in items" :key="item.id" class="item">
        <p class="paragraph">{{ item.title }}</p>
        <div v-if="item.checked" class="items-square">
          <div v-for="childItem in item.childItems" :key="childItem.id">
            <div class="squares" v-if="childItem.checked">
              <div
                v-for="i in childItem.count"
                :key="i"
                class="square"
                :style="`background-color: ${childItem.color}`"
                @click="childItem.count--"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
      default() {
        return [];
      },
    },
  },
};
</script>
<style scoped>
.checkboxes-block-items {
  width: 450px;
  min-height: 450px;
  height: auto;
  border: 2px solid #000;
}
.items {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 30px;
}
.item {
  width: 80%;
  min-height: 60px;
  border: 2px solid #000;
  margin: 10px;
}
.paragraph {
  margin-left: 10px;
}
.items-square {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.square {
  width: 13px;
  height: 13px;
  margin: 0px 5px 5px 5px;
}
.squares {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
}
</style>
