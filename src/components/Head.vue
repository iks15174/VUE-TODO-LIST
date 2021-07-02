<template>
  <div id="head">
      <b-card :title="getTitle" :sub-title="getSubTitle"></b-card>
  </div>
</template>

<script>
const dayStr = ["월", "화", "수", "목", "금", "토", "일"]
export default {
  name: 'Head',
  data(){
      return{
          today : new Date(),
      }
  },
  computed: {
      getTitle(){
          return this.today.getFullYear() + "년 " + (this.today.getMonth()+1) + "월 " + this.today.getDate() + "일";
      },
      getSubTitle(){
          return dayStr[this.today.getDay() - 1] + "요일";
      }
  }
}
</script>

<style>
#head{
    text-align: center;
}
</style>