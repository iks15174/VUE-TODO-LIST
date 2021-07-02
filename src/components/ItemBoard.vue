<template>
  <div>
    <b-list-group>
        <Item v-for="item in items" :key="item.id" :item="item" @delete="deleteItem"></Item>
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
      }
  }
}
</script>

<style>
</style>