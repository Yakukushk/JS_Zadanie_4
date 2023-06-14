<script>
export default{
props: ['elements'],
data() {
    return {
      newElement: {
        title: '',
        Price: '',
        description: '',
        open: false
      },
      editingElement: null
    };
  },
  methods : {
    addNewElement() { // method for adding new element 
      if (this.editingElement) {
        
        this.editingElement.title = this.newElement.title;
        this.editingElement.description = this.newElement.description;
        this.editElement.Price = this.newElement.Price;
        this.editingElement = null;
      } else {
       
        this.elements.push({ ...this.newElement, open: false });
      }
      this.resetForm();
      this.saveElements();
      console.log("add element" + this.addNewElement)
    }, 
    deleteElement(index){ // method for deleting new element 
       this.elements.splice(index, 1);
       this.saveElements();
       console.log("delete element" + this.deleteElement)
    },
    editElement(element){ // method for editing new element 
        this.newElement.title = element.title;
        this.newElement.description = element.description;
        this.newElement.Price = element.Price;
        this.editingElement = element;
        console.log("edit element" + this.editElement)
    },
    resetForm() { // method for reseting new element 
        this.newElement.title = "";
        this.newElement.description = "";
        this.newElement.Price = 0;
        console.log("reset element" + this.resetForm)
    },
    toggleElement(element) {
        element.open =  !element.open;
        this.saveElements();
        console.log("toogle element" + this.toggleElement)
    },
    saveElements() { // method for saving new element 
      localStorage.setItem('elements', JSON.stringify(this.elements));
      console.log("save element" + this.saveElements)
    }


  }
}

</script>


<template>
<div>
<form @submit.prevent="addNewElement"> 
    <div class="mb-3 mt-2">
<label for="exampleInputTitle" class="form-label"></label>
<input type="text" v-model="newElement.title" placeholder="Type your title" required>
</div>
<div class="mb-3">
<input type="text" v-model="newElement.description" placeholder="Type your Description" required>
</div>
<div class="mb-3">
<input type="number" v-model="newElement.Price" placeholder="Type your Price" required>
</div>
<div class="mb-3">
<button type="reset" @click="resetForm" class="btn btn-secondary btn-sm">Reset</button>
</div>
<button type="submit" class="btn btn-primary btn-sm">Add New Element</button>
</form>
<ul class="list-group mt-4">
      <li v-for="(element, index) in elements" :key="index">
        <div class="mb-2">
        <h3 @click="toggleElement(element)">{{ element.title }}</h3>
         </div>
         <div class="mb-2">
        <h4>{{ element.Price }}zł</h4>
        </div>
        <p v-if="element.open">{{ element.description }}</p>
        <div class="mb-2">
        <button class="btn btn-danger btn-sm" @click="deleteElement(index)">Delete</button>
        </div>
        <button class="btn btn-success btn-sm" @click="editElement(element)">Edit</button>
      </li>
    </ul>
</div>
</template>



<style scoped>



</style>