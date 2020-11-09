<template> 
<v-form @submit.prevent="addItem">
    <v-container>
      <v-row justify="center">
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
          outlined
          shaped
            v-model="item.title"
            label="What are you grateful for?"
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

