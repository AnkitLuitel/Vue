<script setup>
  import { ref } from 'vue';
  const showModal = ref (false);
  const newNotes = ref("");
  const notes = ref([]);
  //dsfjds
  const getRandomColor=()=> {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
  const addNotes= () => {
    notes.value.push({
      id: Math.floor(Math.random()*100000),
      text : newNotes.value,
      date: new Date(),
      color: getRandomColor()
    });
   showModal.value = false;
   newNotes.value=""
  }


</script>
<template>
  <div v-if="showModal"  class="overlay bg-neutral-700 z-10 w-screen h-screen absolute flex justify-center items-center">
    <div class="modal sm:w-[600px] w-100 h-max-content bg-white rounded-md p-4">
      <div class="modal-header border-b flex justify-between items-center pb-3"> 
        <div  class="modal-title font-bold text-lg">Add Notes</div>
        <div  @click="showModal=false" class="cancel w-6 h-6 rounded-full shadow-md bg-red-500 flex justify-center items-center text-[15px] text-white cursor-pointer ">x</div>
      </div>
      <div class="modal-body py-3 border-b">
          <textarea v-model="newNotes" class="w-full min-h-[100px] focus:outline-none focus-ring focus:ring-red-400 border p-3"  name="" id=""></textarea>
      </div>
      <div class="modal-footer py-3">
        <div class="button-group flex gap-3">
            <button @click="addNotes"  class="px-3 py-2 bg-green-500 rounded-md text-white">Add Notes</button>
            <button  @click="showModal=false" class="px-3 py-2 bg-red-500 rounded-md text-white"> Cancel</button>
          </div>
      </div>
    </div>
  </div>

  <main class="p-5 flex justify-center pt-40">
    <div class="container px-6 pb-4 shadow-md rounded-md border">
      <div class="">
        <div class="header flex justify-between items-center border-b py-2">
          <div class="title text-[40px]">Notes</div>
          <div @click="showModal=!showModal" class="add_btn w-10 h-10 shadow-md rounded-full p-1 flex justify-center items-center bg-green-400 text-lg cursor-pointer hover:bg-green-600 duration-1000">+</div>
        </div>
        <div class="note-body min-h-[50vh] py-5 grid xl:grid-cols-7 md:grid-cols-4 sm:grid-cols-2 grid-cols-1 gap-4">
            <div :style="{backgroundColor: note.color}"  v-for="note in notes" class="notes-box w-full  h-[200px] shadow-md rounded-lg  cursor-pointer flex flex-wrap overflow-hidden">
              <div  class="content flex flex-col justify-between  h-full p-4 ">
                <div class="para  text-sm ">{{ note.text }}</div>
                <div class="date text-xs font-bold">{{ note.date.toLocaleDateString("en-Us")  }}</div>
              </div>
            </div>
        </div>
      </div>
    </div>
  </main>
</template>
