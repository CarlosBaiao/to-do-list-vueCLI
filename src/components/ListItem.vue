<template>
  <li>
    <span class="container">
      <input
        type="checkbox"
        :id="index"
        class="checkbox"
        v-model="item.checked"
      />
      <label :for="index" @ :class="getItemChecked(item.checked)">{{
        item.label
      }}</label>
    </span>
    <span
      class="iconDelete"
      v-html="deleteIcon"
      @click="deleteItem(index)"
    ></span>
  </li>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "ListItem",
  props: {
    item: Object,
    index: Number,
  },
  computed: {
    deleteIcon() {
      return feather.icons.trash.toSvg({ width: 20 });
    },
  },
  methods: {
    getItemChecked(itemChecked) {
      return itemChecked ? "item-checked" : "";
    },
    deleteItem(index) {
      this.$emit("delete-item", index);
    },
  },
};
</script>

<style scoped lang="less">
li {
  display: flex;
  align-items: center;
  justify-content: space-between;

  background: white;
  padding: 10px 15px;
  border-radius: 5px;
  margin: 10px 0;

  .container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    overflow: auto;
    

    .checkbox {
      margin-right: 10px;
      accent-color: @orange;
    }


    .item-checked {
      &::after {
        content: 'feito';
        text-decoration: none;
        background: @orange;
        margin-left: 10px;
        padding: 0 6px;
        border-radius: 5px;
        color: white;
        
        
      }
    }
  }

   .iconDelete {
      cursor: pointer;
      display: flex;
      align-items: center;
      padding-left: 10px;
    
    }
}
</style>
