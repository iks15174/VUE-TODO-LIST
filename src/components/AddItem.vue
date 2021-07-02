<template>
  <div>
    <b-input-group>
      <b-form-input v-model="text" placeholder="Add todo-list" @keyup.enter="addItem"></b-form-input>
      <b-button variant="outline-primary" @click="addItem">
        <b-icon-plus></b-icon-plus>
      </b-button>
    </b-input-group>
  </div>
</template>

<script>
export default {
  name: "AddItem",
  data() {
    return {
      text: "",
    };
  },
  methods: {
      addItem(){
          if(this.text !== ""){
              this.$emit('addItem', this.text);
              this.text=""
          }
      }
  }
};
</script>

<style>
</style>