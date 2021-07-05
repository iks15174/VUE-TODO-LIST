<template>
  <span>
    <b-list-group-item v-if="!updateMode">
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
      <b-icon-x-circle class="icon" font-scale="1.2" variant="danger" @click="deleteItem"></b-icon-x-circle>
      <b-icon-pencil class="icon" font-scale="1.2" variant="primary" @click="changeToUpdate"></b-icon-pencil>
      <div class="text-primary">{{ diffDays }}일 남았습니다.</div>
    </b-list-group-item>

    <b-list-group-item v-else>
      <b-input-group>
        <b-form-input
          :state="inputState"
          v-model="item.text"
          placeholder="Add todo-list"
          @keyup.enter="addItem"
        >
        </b-form-input>
        <b-button variant="outline-primary" @click="updateItem">
          <b-icon-pencil></b-icon-pencil>
        </b-button>
      </b-input-group>
      <b-form-datepicker
        id="item.id"
        v-model="item.date"
        :value-as-date="true"
        :state="dateState"
        class="mb-2"
      ></b-form-datepicker>
    </b-list-group-item>
  </span>
</template>

<script>
const oneDay = 24 * 60 * 60 * 1000;
export default {
  name: "Item",
  data(){
    return{
      updateMode : false,
      inputState: null,
      dateState: null,
    }
  },
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
    },
    changeToUpdate(){
      this.updateMode = true;
    },
    updateItem(){
      let now = new Date();
      if(this.item.date === null || this.item.date.setHours(0, 0, 0, 0) < now.setHours(0, 0, 0, 0)){
        this.dateState = false;
        return;
      }
      else this.dateState = true;
      if(this.item.text === ""){
        this.inputState = false;
        return;
      }
      this.$emit("update", this.item);
      this.inputState = null;
      this.dateState = null;
      this.updateMode = false;
    }
  },
  computed: {
    diffDays(){
      return Math.round(Math.abs(((new Date()) - this.item.date) / oneDay))
    }
  }
};
</script>

<style>
.icon{
  float: right;
}
</style>