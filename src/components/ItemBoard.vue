<template>
  <div>
    <b-list-group>
        <Item v-for="item in items" :key="item.id" 
        :item="item" 
        @delete="deleteItem"
        @update="updateItem"
        ></Item>
    </b-list-group>
  </div>
</template>

<script>
import Item from "@/components/Item.vue";

export default {
  name: 'ItemBoard',
  components: {Item},
  props: {
      items: {
          type: Array,
          required: true
      }
  },
  methods: {
      deleteItem(id){
          this.$emit("deleteItem", id);
      },
      updateItem(item){
        this.$emit("updateItem", item);
      }
  }
}
</script>

<style>
</style>