<script>
export default{
   data() {
      return {
         itemName: null
      }
   },
   methods: {
      submitForm() {
         this.$emit('onSubmit', this.itemName)
         this.itemName = null
      }
   }
}
</script>

<template>
   <form @submit.prevent="submitForm">
      <input v-model="itemName" />
      <button type="submit">Add new Todo item</button>
   </form>
</template>
