<script>
import CollapsibleList from './components/CollapsibleList.vue';

export default{
  components: {
    CollapsibleList
  }, 
  data(){
      return{
        elements: []
      };
  } ,
  mounted() {
    const storedElement = localStorage.getItem('elements');
    if(!storedElement){
         this.elements = [
          {title: 'Element 1', description: 'Description', open: false},
          {title: 'Element 2', description: 'Description', open: false},
          {title: 'Element 3', description: 'Description', open: false},
          {title: 'Element 4', description: 'Description', open: false},
          {title: 'Element 5', description: 'Description', open: false}
        ]
    }  
  }
}
</script>

<template>
  <div>
    <collapsible-list :elements="elements"></collapsible-list>
  </div>
</template>

<style scoped>

</style>
