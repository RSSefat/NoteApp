
<script setup>

  import {ref} from 'vue'
   
   const showModal = ref(false)
   const newNote = ref("")
   const notes = ref([])  
   const noteTitle = ref()  
   const openCard = ref(false) 
   const cardBtn = ref(false) 
   const showIcon = ref(false) 

  


   const addNote = () => {
      notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: "hsl(" + Math.random() * 360 + ", 100%, 70%)",
      openCard: openCard.value,
      cardBtn: cardBtn.value,
      showIcon: showIcon.value,
      Title: noteTitle.value,
     
        });
     
    showModal.value = false
    newNote.value = ""
    noteTitle.value = ""
    
   
      }

  
    const deleteNote = (index) => {
      notes.value.splice(index, 1)
    }
  
  
</script>
<template>
  <main>
    <div v-if="showModal"   class="overlay">
      <div class="modal">
        <textarea v-model="noteTitle" name="note" id="note" placeholder="Title" cols="1" rows="2"></textarea>
        <textarea v-model="newNote" name="note" id="note" cols="1" rows="10"></textarea>
        <span>
        <button  @click="addNote()" v-if="!edit">Add Note</button>
      
      </span>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>
     
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="cards-container" >
        <div v-for="(note , index) in notes" :key="note.id" @mouseover="note.showIcon = true" @mouseleave="note.showIcon = false " :class="{toggleCard: note.openCard}" :id="note.id"  class="card" :style="{backgroundColor: note.backgroundColor}">
          <h3>{{note.Title}}</h3>
          <p class="main-text"> {{note.text}}</p>
      
          <div  class="cardBtn" :class="{cardButton: note.cardBtn}" v-show="note.showIcon">
         
            <span class="date">{{note.date.toLocaleDateString("en-US")}}</span>
          <div >
            <button @click="deleteNote(index)">
              <font-awesome-icon icon="fa-solid fa-trash-can" />
            </button>
           
            <span @click="note.openCard =!note.openCard" >
              <button v-if="!note.openCard">
                <font-awesome-icon icon="fa-solid fa-eye" />
              </button>
              <button  v-if="note.openCard">
                <font-awesome-icon icon="fa-solid fa-eye-slash" />
              </button>
            </span>
          </div>
          </div>
 
          
        </div>
  
      </div>
    </div>
  </main>
</template> 
<style scoped>
.main{
  margin: 0;
  height: 100vh;
  width: 100vw;
}
.container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h1{
    font-weight: bold;
    font-size: 50px;
  }
  header button{
    border: none;
    padding: 10px ;
    width: 40px;
    height: 40px;
    cursor: pointer;
    background-color: rgb(21,20,20);
    color: white;
    border-radius: 100%;
  }
  .card{
    width: 200px;
    height: 200px;
    background-color: rgb(167, 100, 12);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between ;
    margin-right: 30px;
    margin-bottom: 40px;
    overflow:hidden;

   
  }
  .card h3{
    margin-bottom: -48px;
  }
 
  .cards-container{
    display: flex;
    flex-wrap: wrap;
   max-width: 1000px;
    
  }
  .date{
    font-size: 10.5px;
    font: bold;
    display: flex;

  }
  .overlay{

    position: absolute;
   height: 100%;
   width: 100%;

    background-color: rgba(0,0,0,0.77);
   
    display:flex;
    align-items: center;
    justify-content: center;


  }
  .modal{
    width: 750px;
    background-color:white ;
    border-radius: 10px;
    position: relative;
    display: flex;
    flex-direction: column;
    padding: 15px;
  }
  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border:none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  
  }
  .modal .close{
    background-color: rgb(199, 80, 80);
  }
  
  .toggleCard{
   padding: 20px;
    position: absolute;
   height: 60%;
   width: 100vh;
   display:flex;
   
    justify-content: space-between;
  }
  .toggleCard h3{
    margin-bottom: -10%;
  }
  .cardBtn,   .cardButton{
    display: flex;
    justify-content: space-between;
    
    
  
  }
.cardBtn div button ,.cardbtn span button{
  border: none;
  background: transparent;

}


</style>>
