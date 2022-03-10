<template>
  <div class="checkboxes-block">
    <ul class="checkbox-list">
      <li class="checkbox-list__item" v-for="item in array" :key="item.id">
        <span
          :class="item.isOpen ? 'mdi mdi-minus icon' : 'mdi mdi-plus icon'"
          @click="isOpenedCheckbox(item)"
        ></span>
        <input
          type="checkbox"
          :name="item.title"
          :id="item.title"
          :checked="item.checked"
          @change="checkedItem(item)"
        />
        <label :for="item.title">{{ item.title }}</label>
        <ul class="child-list" v-if="item.isOpen">
          <li
            class="child-list__item"
            v-for="childItem in item.childItems"
            :key="childItem.id"
          >
            <div>
              <input
                type="checkbox"
                :name="childItem.title"
                :id="childItem.title"
                :checked="childItem.checked"
                @change="checkedChildItem(childItem, item)"
              />
              <label :for="childItem.title">{{ childItem.title }}</label>
            </div>

            <div class="child-item">
              <p
                @click="childItem.isInputOpen = !childItem.isInputOpen"
                class="paragraph"
              >
                {{ childItem.count }}
              </p>
              <input
                v-if="childItem.isInputOpen"
                class="input-count"
                type="text"
                v-model.number="childItem.count"
                @keyup.enter="childItem.isInputOpen = false"
              />
              <input
                class="input-color"
                type="color"
                v-model="childItem.color"
              />
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data: () => ({
    input: false,
    array: [],
  }),
  methods: {
    isOpenedCheckbox(item) {
      item.isOpen = !item.isOpen;
      console.log(item);
    },
    checkedItem(item) {
      item.checked = !item.checked;
      if (item.checked) {
        item.childItems.map((childItem) => (childItem.checked = true));
      } else {
        item.childItems.map((childItem) => (childItem.checked = false));
      }
      this.$emit("checkeds", this.array);
    },
    checkedChildItem(childItem, item) {
      childItem.checked = !childItem.checked;
      this.$emit("checkeds", this.array);
      const checkbox = item.childItems.filter((item) => item.checked === false);
      if (checkbox.length === item.childItems.length) {
        item.checked = false;
      } else {
        item.checked = true;
      }
    },
  },
  computed: {
    checkboxes() {
      return array;
    },
  },
  mounted() {
    let array = [];
    let counterID = 1;
    let couterTitle = 1;
    let counterChildItemID = 1;
    let counterChildItemTitle = 1;
    const colors = ["#26F232", "#26FF67", "#234562", "#345344"];
    for (let i = 0; i < 3; i++) {
      array.push({
        id: `${counterID++}`,
        title: `List ${couterTitle++}`,
        checked: false,
        isOpen: false,
        childItems: [],
      });
    }
    array.forEach((item) => {
      for (let j = 0; j < 3; j++) {
        item.childItems.push({
          id: `${counterChildItemID++}`,
          color: `${colors[Math.floor(Math.random() * colors.length)]}`,
          title: `Item ${counterChildItemTitle++}`,
          count: Math.floor(Math.random() * 30),
          checked: false,
          isInputOpen: false,
        });
      }
    });
    this.array = array
    this.$emit("checkeds", this.array);
  },
};
</script>
<style scoped>
.checkboxes-block {
  min-width: 450px;
  min-height: 450px;
  height: auto;
  border: 2px solid #000;
}
.checkbox-list__item {
  list-style: none;
}
.child-list {
  margin-top: 10px;
}
.child-list__item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 70%;
  height: 30px;
}
.icon {
  cursor: pointer;
}
.child-item {
  display: flex;
  flex-direction: row;
}
.input-color {
  position: relative;
  bottom: 4px;
  outline: none;
  border: none;
  width: 25px;
  height: 25px;
  margin-bottom: 10px;
  padding: 0;
  background-color: #fff;
}
.paragraph {
  margin: 0px 10px 0px 0px;
  padding: 0;
  cursor: pointer;
}
.input-count {
  width: 30px;
  height: 13px;
}
</style>
