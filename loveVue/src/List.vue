<script>
export default{
    props:{
        data:{ type:Array, required:true}
    },
    methods:{
      eventHandler: function(e){
        e.preventDefault()
        console.log(e.target.innerHTML, e.target.getAttribute('href'))
        this.description=e.target.getAttribute('href') 
      }
    },
    data() {
        return {description: ''} 
    }, 
}
</script>
<template>
    <ul>
        <li  v-for="item in data" :key="item.id"> 
            <a :href="item.description" @click.pervant="eventHandler">{{ item.title }} </a>
        </li>    
    </ul>
    <br>
    <div>{{ description }}</div>    
</template>

<style scoped> 
 ul {
    background-color: lightblue;
    color: red; 
 } 
 ul li {
    float: left;
    margin: 20px;
 } 
 div{
    text-align: center;
 }
</style>
