<template>
  <div class="markdown-body">
    <p class="text-2xl pb-5 p-5 ms-5 text-sans text-white text-start">
      Inventory
    </p>
    <div class="p-5">
      <div v-if="inventory.length == 0">
        <span class="text-white text-start"
          >Sorry, there are no items here yet</span
        >
      </div>
      <div v-else>
        <div class="wrapper">
          <div v-for="item in inventory" class="item">
            <div class="bg-white text-center rounded mb-5">
              <p class="p-5">{{ getName(item) }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { getItems } from "@theme/utils/helpers";
const items = require("@theme/utils/items.json");
import { emitter } from "@theme/utils/emitter";

export default {
  name: "Inventory",

  data() {
    let obj = { inventory: [] };
    return obj;
  },
  methods: {
    showInventoryItems() {
      var ids = getItems();
      this.inventory = ids.map((id) => items.find((item) => item.id == id));
    },

    getName(item) {
      if (item) {
        let currItem = item.name;
        return currItem;
      }
      else return false
    },
    
  },
  created() {
    this.showInventoryItems();
    emitter.on("item_added", (id) => {
      this.showInventoryItems();
    });
  },
};
</script>