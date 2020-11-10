
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
      box-shadow="24"
      class="rnd"
   />
   <v-card-title >I am Grateful for:</v-card-title>
  
    <v-list >
          <v-sheet
  color="gray darken-2"
  elevation="6"
  outlined
  rounded
>
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
 <transition name="view">
            <h3 draggable="true" @dragstart="startDrag($event,item)"
            v-if="show">
            {{item.title}}</h3>
 </transition>

              <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
      :retain-focus="false"
    >
     
      <v-card>
        <v-card-title class="secondary">
          You are Grateful for:
        </v-card-title>

        <v-card-text>
            <!-- <transition name="view">
            <h3 draggable="true" @dragstart="startDrag($event,item)"
            v-if="show">
            {{item.title}}</h3>
 </transition> -->
         <h3> {{newestTitle}}! <v-divider/>There is something good out there, after all!</h3>

        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = !dialog"
          >
            Exit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
    
            <v-divider></v-divider>
            
          </v-list-item-content>
          
                <v-divider
  vertical
></v-divider>
              <v-icon
        small
        right
        
      >
        mdi-calendar-clock
        
      </v-icon>
      :
      <v-divider
  vertical
></v-divider>
 {{item.date}}
<v-divider
  vertical
></v-divider>
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
        </v-sheet>
    </v-list>
    <v-btn
            color="primary"
            text
            @click="listDisplay = !listDisplay"
          >
            Display Just The List!
          </v-btn>
           <div class="text-center">
    <v-dialog
      v-model="listDisplay"
      width="500"
      :retain-focus="false"
    >
     
      <v-card>
        <v-card-title class="secondary">
          All The Things You're Grateful For:
        </v-card-title>
<v-list>
          <v-sheet
  color="gray darken-2"
  elevation="6"
  outlined
  rounded
>

<v-list-item-group
        color="primary"
      >
        <v-list-item
          v-for="(item) in listOne"
          :key="item.title"
          
        >
          <v-list-item-content>
 
            <h3>
            {{item.title}}</h3>

         
          </v-list-item-content>
        </v-list-item>
</v-list-item-group>
          <v-btn
            color="primary"
            text
            @click="listDisplay= !listDisplay"
          >
            Exit
          </v-btn>
          </v-sheet>
          </v-list>
      </v-card>
    </v-dialog>
  </div>

  <v-divider/>
  <v-sheet
  color="gray darken-2"
  elevation="24"
  outlined
  rounded>
  <div>
      
      <v-row justify="center">
             
          <v-chip
  color="primary"
  dark
  class="rnd"
>
      <h2 >Ideas:</h2>
      </v-chip>
      </v-row>
      </div>
      <div>
      <v-row justify="center">
      <h5>(Drag and drop into Gratitude List)</h5>
      
      </v-row>
      
      </div>
  </v-sheet>
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
import moment from 'moment'
  export default {
      
    data: () => ({
        listDisplay: false,
        dialog:false,
        show: false,
        newestTitle:"",
      items: [
        //   {title:"Friends", list:1},
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
           this.items.push({title:item, list:1, date: moment().format("MMM Do YY")})
           this.dialog = !this.dialog
           this.newestTitle = item
       },
       newIdea(item){
           this.items.push({title:item, list:2,date: moment().format("MMM Do YY")})
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
    this.$nextTick(() => {
    this.show = true
  })
    
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

<style scoped>
.view-leave-active {
    transition: opacity 0.5s ease-in-out, transform 0.5s ease;
}

.view-enter-active {
    transition: opacity 0.5s ease-in-out, transform 0.5s ease;
    transition-delay: 0.5s;
}

.view-enter, .view-leave-to {
    opacity: 0;
}

.view-enter-to, .view-leave {
    opacity: 1;
}
.rnd{
    border-radius:50px;
}
</style>