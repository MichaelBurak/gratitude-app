
<template>
<div>
  <v-card
    class="mx-auto"
    max-width="300"
    tile
  >
  <divider></divider>
  <v-img
      src="../assets/gabrielle-henderson-Y3OrAn230bs-unsplash.jpg"
      height="300px"
      dark
   />
   <v-card-title>I am Grateful for:</v-card-title>
    <v-list >
        
      <v-list-item-group
        color="primary"
      >
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
        >
          <v-list-item-content>
              
            <v-list-item-title v-text="item.title">
            </v-list-item-title>
              
              
            <h3 v-if="item.showText"> {{item.text}} </h3>
            <divider></divider>
            <v-row justify="center">
          <!-- <v-btn
          x-small
          light
          @click="item.showText = !item.showText"
       > Remind yourself why. </v-btn> -->
            </v-row>
          </v-list-item-content>
          
          
              <v-divider></v-divider>
              
          
        </v-list-item>
      </v-list-item-group>
    </v-list>
    
  </v-card>
  <ItemForm @newItem="newItem"/>
  </div>
  
</template>

<script>
import ItemForm from "./ItemForm"
  export default {
    data: () => ({
      items: [
        // { title: 'Friends', avatar:"https://i.imgur.com/iAcIdXW.jpg", text: "I am grateful because they've stayed by my side.", showText: false},
        // {title: "Myself", avatar:"https://i.imgur.com/cZsxGQ7.jpg", text: "I am grateful because I have learned to be my own advocate.", showText: false}
      ]
   }),
   components: {ItemForm},
   methods:{
       newItem(item){
           this.items.push({title:item})
       }
   },
   mounted() {
    console.log('App mounted!');
    console.log(JSON.parse(localStorage.getItem('items')))
    if (localStorage.getItem('items')) this.items = JSON.parse(localStorage.getItem('items'));
  },
  watch: {
    items: {
      handler() {
        console.log('items changed!');
        localStorage.setItem('items', JSON.stringify(this.items));
      },
      deep: true,
    }
  }

  }
</script>
