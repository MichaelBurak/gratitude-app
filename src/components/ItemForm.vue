<template> 
<v-form @submit.prevent="addItem">
    <v-container>
      <v-row justify="center">

          <v-text-field v-if="type === 'newItem'"
          shaped
            v-model="item.title"
            label="What are you grateful for?"
            background-color="primary"
            dark
            required
            filled
          ></v-text-field>
          
          <v-text-field v-else-if="type === 'newIdea'"
          shaped
            v-model="item.title"
            label="Any ideas? Enter here:"
            required
            filled
          ></v-text-field>
          
      </v-row>
    </v-container>
  </v-form>
  </template>


<script>
  export default {
    name:"ItemForm",
    props:['type'],
    data: () => ({
     item: {title:""},
     newItems: [

     ]
   }),
   methods: {
         addItem() {
        this.$emit("newItem", this.item.title, this.item.date)
         }
   }
  }
</script>

