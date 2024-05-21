<script setup>
import Modal from '@/components/Modal.vue';
import { ref, watch  } from 'vue';
import {uid} from 'uid'
import NoteItem from '@/components/Note-Item.vue';
import {Icon} from '@iconify/vue'


const showModal = ref(false)

const Lists = ref([])

watch(Lists, ()=>{setLocalStorage();}, {deep:true})

const fetchList = () => {
  const saveList = JSON.parse(localStorage.getItem("list"))
  if (saveList) {
  Lists.value = saveList;
  }
}

fetchList();

const setLocalStorage = ()=> {
  localStorage.setItem("list", JSON.stringify(Lists.value))
}

function getRandomColor(){
  return "hsl("+ Math.random() * 360 +" , 100% , 75%)";
}

const createLists = (text) => {
  Lists.value.push(
    {
      id:uid(),
      text,
      date:new Date(), 
      notecolor:getRandomColor(),
      isEditing:null,
      isComplete:null
    }
  )
  
}

const updateList = (val, pos) => {
  Lists.value[pos].text = val
}

const editList = (pos) => {
  Lists.value[pos].isEditing = !Lists.value[pos].isEditing
}


const deleteList = (noteId) => {
  Lists.value = Lists.value.filter((text) => text.id !== noteId)
}
</script>


<template>
  <main>

    <Modal v-model:close="showModal" v-if="showModal" @create = "createLists"/>

    <div class="homeview">
      <div class="items">
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </div>

      <ul>
        
        <NoteItem v-if="Lists.length > 0" class="notes" v-for="(note, index) in Lists" :noteprop="note" :indexprop="index" 
        :style="{backgroundColor:note.notecolor}"
        @update = "updateList"
        @edit="editList"
        @delete="deleteList"/>

        <p v-else class="sad">
          <Icon icon="noto-v1:sad-but-relieved-face" width="20"/>
          <span>No Notes Yet! Add Some. </span>
        </p>
        
      </ul>
    </div>
   
  </main>
</template>


<style lang="scss" scoped>
  main{
    max-width: 950px;
    margin: 2rem auto;

    
    .items{
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-content: center;
      align-items: center;

      button{
        width: 30px;
        height: 30px;
        border-radius: 50%;
      }
    }

    ul{
      display: flex;
      flex-wrap: wrap;
      margin-bottom: 10px;

    }
  }
</style>