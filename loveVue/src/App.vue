<script>
import List from './List.vue'
  export default{
    components:{
      List
    },
    data(){
      return{
        data: [
         {
          id:1,
          title: "Chess",
          url:"https://www.chess.com",
          description:"Chess"
         },
         {
          id:2,
          title: "Youtube",
          url:"https://www.youtube.com/",
          description:"Youtube",
         } ,
         {
          id:3,
          title: "Chrome",
          url:"https://www.google.com/search?channel=fs&client=ubuntu&q=chrome",
          description: "Chrome",
         },
        ]
      }
    
    } 
    
  }
</script>
<template>
  <List :data="data"/>
</template>