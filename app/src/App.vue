<script setup>
import {ref} from 'vue'
import ListCard from '@/components/ListCard.vue';
const lists = ref([
  { name: "Your First List", tasks: ["Press the Plus Button", "Create a New List"], id: 1},
])

const newTasks = ref([""]);
const listName = ref("");
const listId = ref(2);
const selectedList = ref(null)


function openModal() {
  const modal = document.getElementById('NewListModal');
  modal.classList.remove('hidden');
  listName.value = "";
  newTasks.value = [""];   
}

function closeModal(id){
  const modal = document.getElementById(id);
  modal.classList.add('hidden');
}
function addNewTask(){
  newTasks.value.push("");
}
function createNewList(){
  const tasks = newTasks.value;
  lists.value.push({ name: listName.value, tasks: tasks, id: listId.value });
  listId.value++;
  closeModal('NewListModal');
}

function view(list){
  selectedList.value = list;
  const viewModal = document.getElementById('viewTheList');
  viewModal.classList.remove('hidden');
}

function deleteList(deletedList){
  lists.value = lists.value.filter(list => list.id !== deletedList.id);
};

console.log(selectedList);
</script>


<template>
  <div class = "headings flex flex-col gap-2 mt-8 text-center items-center">
  <h1 class = "text-6xl font-gummy text-black text-shadow-md tracking-widest">To Do!</h1>
  <h2 class = "text-4xl font-fancy text-sky-200 tracking-wide">pls do yo work</h2>
  <hr class="border-gray-400 border-1 border-dotted w-300 my-4">
  </div>

  <div class = "mt-5 menu2 flex justify-center gap-7">
  <h2 class = "your lists text-5xl font-gummy text-sky-200 tracking-wide text-center">Your Lists</h2>
  <button class="bg-emerald-200 hover:bg-emerald-300 text-white text-2xl font-bold py-1 px-4 rounded" @click="openModal()">+</button>
  </div>
  <div class = "listcontainer flex justify-center gap-4 mt-10">
  <ListCard v-for= "list in lists" :key="list.name" :list="list" @viewlist="view" @deletelist="deleteList">{{list.name}}</ListCard> 
  </div>
      <div id="NewListModal" class="fixed inset-0 bg-black/75 flex items-center justify-center hidden">
        <div class="bg-sky-50 p-8 rounded-lg shadow-xl w-auto h-150 border-2 border-slate-300 overflow-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-5xl text-sky-200 font-fancy font-semibold">Create New List</h2>
                <button @click="closeModal('NewListModal')" class="text-gray-500 text-5xl hover:text-gray-700">
                    &times;
                </button>
            </div>
            <div class="flex flex-col gap-2">
                <input type="text" placeholder="List Name" v-model="listName" class="font-gummy w-full p-2 mb-4 border border-gray-300 rounded">
                <input v-for="(task, index) in newTasks" :key="index" type="text" :placeholder="'Task ' + (index + 1)" v-model="newTasks[index]" class="font-gummy w-full p-2 mb-4 border border-gray-300 rounded">

                <button class="bg-emerald-200 font-gummy hover:bg-emerald-300 text-white text-2xl font-bold py-1 px-4 rounded" @click="addNewTask()" >Add New Task</button>
                <button class="bg-emerald-200 font-gummy hover:bg-emerald-300 text-white text-2xl font-bold py-1 px-4 rounded" @click="createNewList()">Create List</button>
            </div>
        </div>
    </div>
    
    <div id="viewTheList" class = "fixed inset-0 bg-black/75 flex items-center justify-center hidden">
      <div class="bg-sky-50 p-8 rounded-lg shadow-xl w-200 h-150 border-2 border-slate-300">
             <div class="flex justify-between items-center mb-4">
                <h2 class="text-5xl text-sky-200 font-fancy font-semibold">{{selectedList?.name}}</h2>
                  <button @click="closeModal('viewTheList')" class="text-gray-500 text-5xl hover:text-gray-700">
                    &times;
                </button>
            </div>
            <div class="flex flex-col gap-5">
                  <ul class="list-disc text-2xl list-inside text-center leading-loose items-left">
                    <li v-for="task in selectedList?.tasks" :key="task">{{ task }}<button class="ml-6 mb-2 bg-rose-200 hover:bg-rose-300 text-white text-sm font-bold py-1 px-2 rounded">Delete</button></li>
                  </ul>
            </div>
      </div>
    </div>
     
    <!-- <div id="viewTheList" class = "fixed inset-0 bg-black/75 flex items-center justify-center hidden">
      <div class="bg-sky-50 p-8 rounded-lg shadow-xl w-200 h-150 border-2 border-slate-300">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-5xl text-sky-200 font-fancy font-semibold">{{selectedList.name}}</h2>
                  <button @click="closeModal('viewTheList')" class="text-gray-500 text-5xl hover:text-gray-700">
                    &times;
                </button>
            </div>
            <div class="flex flex-col gap-5">
                <h3 class="text-2xl font-gummy text-sky-200 tracking-wide"></h3>
                  <ul class="list-disc list-inside text-center leading-loose ">
                    <li v-for="task in selectedList.tasks" :key="task">{{ task }}<button class="ml-2 bg-rose-200 hover:bg-rose-300 text-white text-sm font-bold py-1 px-2 rounded">Delete</button></li>
                  </ul>
            </div>
      </div>
    </div> -->
</template>

<style scoped></style>


