<template>
  <div class="checkboxes-block">
    <ul class="checkbox-list">
      <li class="checkbox-list__item" v-for="item in items" :key="item.id">
        <span
          :class="item.isOpen ? 'mdi mdi-minus icon' : 'mdi mdi-plus icon'"
          @click="item.isOpen = !item.isOpen"
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
    items: [
      {
        id: "1",
        title: "List 1",
        checked: false,
        childItems: [
          {
            id: "1",
            color: "#26F232",
            title: "Item 1",
            count: 10,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "2",
            color: "#26FF67",
            title: "Item 2",
            count: 15,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "3",
            color: "#234562",
            title: "Item 3",
            count: 40,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "4",
            color: "#345344",
            title: "Item 3",
            count: 25,
            checked: false,
            isInputOpen: false,
          },
        ],
        isOpen: false,
      },
      {
        id: "2",
        title: "List 2",
        checked: false,
        childItems: [
          {
            id: "1",
            color: "#26F232",
            title: "Item 1",
            count: 10,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "2",
            color: "#26FF67",
            title: "Item 2",
            count: 15,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "3",
            color: "#234562",
            title: "Item 3",
            count: 40,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "4",
            color: "#345344",
            title: "Item 3",
            count: 25,
            checked: false,
            isInputOpen: false,
          },
        ],
        isOpen: false,
      },
      {
        id: "3",
        title: "List 3",
        checked: false,
        childItems: [
          {
            id: "1",
            color: "#26F232",
            title: "Item 1",
            count: 10,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "2",
            color: "#26FF67",
            title: "Item 2",
            count: 15,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "3",
            color: "#234562",
            title: "Item 3",
            count: 40,
            checked: false,
            isInputOpen: false,
          },
          {
            id: "4",
            color: "#345344",
            title: "Item 3",
            count: 25,
            checked: false,
            isInputOpen: false,
          },
        ],
        isOpen: false,
      },
    ],
    input: false,
  }),
  methods: {
    checkedItem(item) {
      item.checked = !item.checked;
      if (item.checked) {
        item.childItems.map((childItem) => (childItem.checked = true));
      } else {
        item.childItems.map((childItem) => (childItem.checked = false));
      }
      this.$emit("checkeds", this.items);
    },
    checkedChildItem(childItem, item) {
      childItem.checked = !childItem.checked;
      this.$emit("checkeds", this.items);
      const checkbox = item.childItems.filter((item) => item.checked === false);
      if (checkbox.length === item.childItems.length) {
        item.checked = false;
      } else {
        item.checked = true;
      }
    },
  },
  mounted() {
    this.$emit("checkeds", this.items);
  }
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
