<script setup>
  import {ref} from "vue";

  const showModal = ref(false)
  const newNote = ref("")
  const errorMessage = ref("")
  const notes = ref([])

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

  const addNote = () => {
    if(newNote.value.length < 10){
      return errorMessage.value = "At least you need to enter 10 charecters also"
    }
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    });
    showModal.value = false;
    newNote.value = ""
  }

</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10" ></textarea>
        <p v-if="errorMessage">{{errorMessage}}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: notes.backgroundColor}">
          <p class="main-text">{{note.text}}</p>
          <p class="date">{{note.date.toLocaleDateString(en-US)}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main{
    width: 90vw;
    height: 100vh;
  }

  .container{
    max-width: 100%;
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
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: white;
    border-radius: 100%;
    color: rgb(21, 20, 20);;
    font-size: 20px;
    font-weight: bold;
  }

  .card{
    width: 255px;
    height: 255px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    color: black;
  }

  .date{
    color: black;
    font-size: 12.5px;
    font-weight: bold;
  }

  .card-container{
    display: flex !important;
    flex-direction: row;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    width: 90%;
    height: 100%;
    background-color: rgba(185, 185, 185, 0);
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: center;
  }
 
  .modal{
    width: 750px;
    margin: 10px;
    padding: 10px;
    background-color: rgba(223, 223, 223, 0.521);
    border-radius: 10px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  textarea{
    background-color: #e9e9e9;
    color: black;
    font-weight: 450;
  }

  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: rgb(20, 153, 3);
    border: none;
    color: rgb(255, 255, 255);
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close{
    background-color: rgb(193, 15, 15);
    margin-bottom: 10px;
  }

  .modal p{
    color: rgb(193, 15, 15);
  }
</style>