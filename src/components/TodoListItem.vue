<template>
<li>
  <span>
  {{todoItem}}
  </span>
  <button @click="removeTodo">
    삭제
  </button>
</li>
</template>

<script>
export default {
  name: "TodoListItem",
  props:{
    todoItem : {
      type : Array,
      required : false
    },
    index :{
      type : Number,
      required: false,
    }
  },
  methods : {
    removeTodo(){
      this.$emit('remove', this.index)
    }
  }
};
</script>

<style scoped>

</style>