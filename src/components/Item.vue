<template>
  <span>
    <b-list-group-item>
      <b-icon-check-circle
        @click="clickToggle"
        :variant="item.checked ? 'success' : 'dark'"
      ></b-icon-check-circle>
      
      <s id="text" v-show="item.checked">
          {{ item.text }}
      </s>
      <span id="text" v-show="!item.checked">
        {{ item.text }}
      </span>
      <b-icon-x-circle-fill variant="danger" @click="deleteItem"></b-icon-x-circle-fill>
    </b-list-group-item>
  </span>
</template>

<script>
export default {
  name: "Item",
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {
    clickToggle() {
      this.item.checked = !this.item.checked;
    },
    deleteItem(){
        this.$emit('delete', this.item.id);
    }
  },
};
</script>

<style>
#text {
  display: inline-block;
  width: 85%;
}
</style>