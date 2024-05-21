<script setup>
import { reactive, onMounted, nextTick } from "vue"

    const noteList = reactive({
        text:"",
        errMsg:"",
        invalid:null
    })

    const emit = defineEmits(["create", "update:close"])
    

    const createNote = () => {

        noteList.invalid = null;

        if(noteList.text.trim().length <= 0){
            noteList.invalid = true;
            noteList.errMsg = "Notes cannot be empty";  
        }
        else{
            emit('create', noteList.text)
            noteList.text = ""
            emit('update:close', false)
        }
    }

    const handleKeyUp = (event) => {
    if (event.key === 'Enter') {
        event.preventDefault();
        createNote();
    } else if (event.key === 'Escape') {
        emit('update:close', false);
    }
}

onMounted(async () => {
    await nextTick();
    document.querySelector('.modal textarea').focus();
});
</script>

<template>
    <div class="overlay" @keydown="handleKeyUp">
        <div class="modal">
            <textarea v-model="noteList.text" cols="30" rows="10"  
            @keyup.enter="handleKeyUp" 
            :class="{'inp-err':noteList.invalid}"></textarea>
            <p v-show="noteList.invalid" class="error">{{ noteList.errMsg }}</p>
            <div class="buttons">
            <button @click="createNote" class="addnote">Add Note</button>
            <button @click="emit('update:close',false)" class="close">Close</button>
            </div>
        </div>
    </div>
</template>



<style lang="scss" scoped>
    .overlay{
        background-color: rgba(0,0,0,0.5);
        height: 100%;
        position: absolute;
        width: 100%;
        z-index: 1;
        justify-content: center;
        align-items: center;
        display: flex;
        left: 0;

        .modal{
            width: 750px;
            position: relative;
            padding: 30px;
            border-radius: 10px;
            background-color: white;
            display: flex;
            flex-direction: column;

            button{
                padding: 10px 20px;
                font-size: inherit;
                width: 100%;
                background-color: #7bbb7b;
                border: none;
                color: white;
                cursor: pointer;
                margin-top: 10px;

            }
            .close
                {
                    background-color: rgb(221, 77, 77);
                }
        }

        .error{
            color: red;
        }

        .inp-err {
            border-color: red;
        }

        .buttons{
            display: flex;

            .addnote{
                margin-right: 10px;
            }
        }
    }
</style>