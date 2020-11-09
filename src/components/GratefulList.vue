
<template>
<div>
  <v-card
    class="mx-auto"
    max-width="300"
    tile
  >
  <v-divider></v-divider>
  <v-img
      src="../assets/gabrielle-henderson-Y3OrAn230bs-unsplash.jpg"
      height="300px"
      dark
   />
   <v-card-title>I am Grateful for:</v-card-title>
    <v-list >
        <div @drop='onDrop($event, 1)' 
      @dragover.prevent
      @dragenter.prevent>
        
      <v-list-item-group
        color="primary"
      >
        <v-list-item
          v-for="(item) in listOne"
          :key="item.title"
          class="drag-el"
        >
          <v-list-item-content>
<!--               
            <v-list-item-title v-text="item.title">
            </v-list-item-title> -->

            <h3 draggable="true" @dragstart="startDrag($event,item)">{{item.title}}</h3>
  

              <!-- </v-align> -->
    
            <v-divider></v-divider>
            
          </v-list-item-content>
          
          
              
        <v-icon
        small
          right
          @click="removeItem(item.title)"
        >
          mdi-minus-circle
        </v-icon>          
        </v-list-item>
      </v-list-item-group>
        </div>
    </v-list>
  <v-divider/>
  <div>
      <v-row justify="center">
      <h2>Ideas:</h2>
      </v-row>
      </div>
      <div>
      <v-row justify="center">
      <h5>(Drag and drop into Gratitude List)</h5>
      </v-row>
      </div>

  <v-card
      class="mx-auto"
      flat
      tile
    >
      <div v-for='item in listTwo' :key='item.title' class='drag-el'>
            <div
      class='drop-zone'
      @drop='onDrop($event, 2)' 
      @dragover.prevent
      @dragenter.prevent
/>
        <h4 draggable="true" @dragstart="startDrag($event,item)">{{ item.title }}
                 <v-icon
        small
          right
          @click="removeItem(item.title)"
        >
          mdi-minus-circle
        </v-icon>          
        </h4>
           

      </div>
      </v-card>
  </v-card>
  <ItemForm @newItem="newItem" type="newItem"/>
  <ItemForm @newItem="newIdea" type="newIdea"/>
  </div>
  
</template>

<script>
import ItemForm from "./ItemForm"
  export default {
    data: () => ({
      items: [
          {title:"Friends", list:1},
        //   {title:"Drop Items Here:", list:2}
      ]
   }),
   components: {ItemForm},
   computed: {
    listOne () {
      return this.items.filter(item => item.list === 1)
    },
    listTwo () {
      return this.items.filter(item => item.list === 2)
    }
},
   methods:{
       newItem(item){
           this.items.push({title:item, list:1})
       },
       newIdea(item){
           this.items.push({title:item, list:2})
       },
       removeItem (title) {
      this.items = this.items.filter(item => item.title !== title)
    },
    startDrag: (evt, item) => {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemTitle', item.title)
      console.log(`Drag title is ${item.title}`)
},
onDrop (evt, list) {
      const itemTitle = evt.dataTransfer.getData('itemTitle')
      const item = this.items.find(item => item.title == itemTitle)
      console.log(`Drop title is ${item.title}`)
      item.list = list
      console.log(`Dropped with list ${item.list}`)
}
   },
   mounted() {
    
    // console.log(JSON.parse(localStorage.getItem('items')))
    if (localStorage.getItem('items')) this.items = JSON.parse(localStorage.getItem('items'));
  },
  watch: {
    items: {
      handler() {
        
        localStorage.setItem('items', JSON.stringify(this.items));
      },
      deep: true,
    }
  }

  }
</script>
