<template>
  <div>
    <b-input-group>
      <b-form-input
        :state="inputState"
        v-model="text"
        placeholder="Add todo-list"
        @keyup.enter="addItem"
      >
      </b-form-input>
      <b-button variant="outline-primary" @click="addItem">
        <b-icon-plus></b-icon-plus>
      </b-button>
    </b-input-group>
    <b-form-datepicker
      id="datepicker"
      v-model="date"
      :value-as-date="true"
      :state="dateState"
      class="mb-2"
    ></b-form-datepicker>
  </div>
</template>

<script>
export default {
  name: "AddItem",
  data() {
    return {
      text: "",
      date: new Date(),
      inputState: null,
      dateState: null,
    };
  },
  methods: {
    addItem() {
      let now = new Date();
      if(this.date === null || this.date.setHours(0, 0, 0, 0) < now.setHours(0, 0, 0, 0)){
        this.dateState = false;
        return;
      }
      else this.dateState = true;
      if(this.text === ""){
        this.inputState = false;
        return;
      }
      else this.inputState = true;
      this.$emit("addItem", this.text, this.date);
      this.text = "";
      this.date = new Date();
      this.inputState = null;
      this.dateState = null;
    },
  },
};
</script>

<style scoped>
</style>