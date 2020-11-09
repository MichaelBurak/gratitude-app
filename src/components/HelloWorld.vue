
<template>
<v-card>
<v-app-bar
  color="purple"
>

    <v-row>
    <v-col cols="2">
      
    </v-col>
    <v-col class="d-flex justify-space-around">
      <v-toolbar-title class="white--text">What's Good? A Gratefulness App.</v-toolbar-title>
    </v-col>
    <v-col cols="2" class="d-flex justify-end">
      
    </v-col>
    </v-row>
      </v-app-bar>
  <v-card
    class="mx-auto"
    max-width="300"
    tile
  >
  <v-img
      src="../assets/gabrielle-henderson-Y3OrAn230bs-unsplash.jpg"
      height="300px"
      dark
   />
    <v-list dense rounded v-if="display">
      <v-subheader>I am Grateful for:</v-subheader>
      <v-list-item-group
        v-model="selectedItem"
        color="primary"
      >
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
        >
          <!-- <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon> -->
          <v-list-item-content>
            
            <v-list-item-title v-text="item.text">

              
            </v-list-item-title>
             <v-row justify="center">
    <v-dialog
      v-model="dialog"
      max-width="290"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          x-small
          light
          v-bind="attrs"
          v-on="on"
        >
          What's good?
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          Isn't there still some good in the world?
          
        </v-card-title>
<!-- <v-img :src="items[selectedItem].avatar"></v-img> -->
        <v-card-actions>
          <v-spacer></v-spacer>
          
          <v-btn
            color="green darken-1"
            text
            @click="dialog = false"
          >
            Exit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    
  </v-card>
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
            v-model="item.text"
            label="What are you grateful for?"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
  <v-row justify="center">
  <v-list dense rounded v-if="display == false">
      <v-subheader>Adding to my grateful pile:</v-subheader>
      <v-list-item-group
        v-model="selectedItem"
        color="primary"
      >
        <v-list-item
          v-for="(newItem, i) in newItems"
          :key="i"
        >
          <!-- <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon> -->
          <v-list-item-content>
            
            <v-list-item-title v-text="newItem.text">

              
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
  </v-list>
  </v-row>
  <v-row justify="center">
   <v-switch
      v-model="display"
      label="Remember what's good"
    ></v-switch>
  </v-row>
</v-card>

</template>

<script>
  export default {
    data: () => ({
      display: false,
      dialog: false,
      selectedItem: 1,
      items: [
        {text:""},
        { text: 'Friends', avatar:"https://i.imgur.com/iAcIdXW.jpg"},
        {text: "Myself", avatar:"https://i.imgur.com/cZsxGQ7.jpg"}
      ],
     item: {text:""},
     newItems: [

     ]
   }),
//    watch: {
//   items: {
//     handler() {
//       console.log('items changed!');
//       localStorage.setItem('items', JSON.stringify(this.items));
//     },
//     deep: true,
//   },
// },
// mounted() {
//   console.log('App mounted!');
//   if (localStorage.getItem('items')) this.items = JSON.parse(localStorage.getItem('items'));
// },
   methods: {
     addItem() {
        this.items.push({ text: this.item.text});
        this.newItems.push({text: this.item.text})
     }
   }
  }
</script>
