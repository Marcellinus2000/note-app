<script setup>
    import {Icon} from '@iconify/vue'

    const props = defineProps({
        noteprop: {
            type: Object,
            required:true
        },
        indexprop: {
            type: Number,
            required:true
        }
    })

    defineEmits(["update", "edit", "delete"])
</script>

<template>
    <div class="note-card">
        
        <textarea v-if="noteprop.isEditing" cols="30" rows="10" v-model="noteprop.text" />
        
        <span v-else class="main text">{{ noteprop.text }}</span>
        
        <div class="bottom">
            <p class="date">{{ noteprop.date.toLocaleDateString("en-US") }}</p>
            <div class="icons">
                <Icon v-if="noteprop.isEditing && noteprop.text.trim() != ''"
                icon="ph:check-circle" 
                color="#447744" width="20px"
                @click="$emit('edit',indexprop)"/>

                <Icon v-if="!noteprop.isEditing" icon="ph:pencil-simple-fill" 
                color="#447744" width="20px"
                @click="$emit('edit',indexprop)"/>

                <Icon icon="ph:trash-simple-fill" 
                color="red" width="20px"
                @click="$emit('delete',noteprop.id)"/>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>
    .note-card{
        width: 225px;
        height: 225px;
        background-color: rgb(237, 182, 44);
        padding: 10px;
        justify-content: space-between;
        border-radius: 15px;
        display: flex;
        flex-direction: column;
        margin-right: 20px;
        overflow: hidden;
        margin-bottom: 20px;

        .bottom{
            display: flex;
            justify-content: space-between;
            align-items: center;
            
            .date{
            font-weight: bold;
            font-size: 12px;
        }

        .icons{
            opacity: 0;

            &:hover{
                cursor: pointer;
            }
        }

    }
        &:hover{
            .icons{
                opacity: 1;
            }
        }

    }
</style>