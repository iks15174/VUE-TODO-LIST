<template>
  <div id="app">
    <Head></Head>
    <AddItem @addItem="addTodoItem"></AddItem>
    <ItemBoard :items="todoItems" 
    @deleteItem="handleDeleteItem"
    @updateItem="handleUpdateItem"
    ></ItemBoard>
    <Foot 
    :total="totalItems" 
    :completed="completedItems" 
    @removeCompleted="handleRemoveCompleted">
    </Foot>
  </div>
</template>

<script>
import Head from "@/components/Head.vue";
import AddItem from "@/components/AddItem.vue";
import ItemBoard from "@/components/ItemBoard.vue";
import Foot from "@/components/Foot.vue";

export default {
  name: 'App',
  components: {Head, AddItem, ItemBoard, Foot},
  data(){
    return{
      todoItems : [],
    }
  },
  methods: {
    addTodoItem(text, date){
      let itemTemp = {
        id: (this.todoItems.length === 0 ? 0 : (this.todoItems[this.todoItems.length - 1].id + 1)),
        checked: false,
        text: text,
        date : date
      };
      this.todoItems.push(itemTemp);
    },
    handleDeleteItem(id){
      for(let i = 0; i < this.todoItems.length; i++){
        if(this.todoItems[i].id === id){
          this.todoItems.splice(i, 1);
        }
      }
    },
    handleUpdateItem(item){
      for(let i = 0; i < this.todoItems.length; i++){
        if(this.todoItems[i].id === item.id){
          this.todoItems[i].text = item.text;
          this.todoItems[i].date = item.date;
        }
      }
    },
    handleRemoveCompleted(){
      for(let i = 0; i<this.todoItems.length; i++){
        if(this.todoItems[i].checked){
          this.todoItems.splice(i, 1);
          i = i - 1;
        }
      }
    }
  },
  computed:{
    totalItems(){
      return this.todoItems.length;
    },
    completedItems(){
      let result = 0;
      for(let i = 0; i < this.todoItems.length; i++){
        if(this.todoItems[i].checked){
          result++;
        }
      }
      return result;
    }
  }
}
</script>
<style>
#app {
  margin-top: 60px;
  width: 50%;
  margin-left: auto;
  margin-right: auto;
}
</style>
