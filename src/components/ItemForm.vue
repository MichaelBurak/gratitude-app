<template> 
<v-form @submit.prevent="addItem">
    <v-container>
      <v-row justify="center">
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field v-if="type === 'newItem'"
          outlined
          shaped
            v-model="item.title"
            label="What are you grateful for?"
            required
          ></v-text-field>
          <v-text-field v-else-if="type === 'newIdea'"
          outlined
          shaped
            v-model="item.title"
            label="What idea do you have?"
            required
          ></v-text-field>
        </v-col>
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
        this.$emit("newItem", this.item.title)
         }
   }
  }
</script>

