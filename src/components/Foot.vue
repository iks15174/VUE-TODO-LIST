<template>
  <div id="foot">
    <b-card class="text-center">
      <div class="text-success">
        {{ total }}개중 {{ completed }}개 완료했습니다.
      </div>
      <b-button @click="removeCompleted" 
      size="sm" 
      variant="outline-success">
      remove completed</b-button>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "Foot",
  props: {
    total: {
      type: Number,
      default: 0,
    },
    completed: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    removeCompleted() {
      this.$emit("removeCompleted");
    },
  },
};
</script>

<style>
</style>