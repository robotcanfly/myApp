<script setup>
    import { ref, onMounted } from 'vue'
    import { useBookStore } from '../stores/book';
    import { RouterLink } from 'vue-router';
    import axios from 'axios'
    const bookStore = useBookStore();


    const loaddata=async()=>{
        try{
            await axios.get(`http://116.206.127.158:3001/api/users/1`,{

            })
            .then((resp)=>{
                console.log(resp.data);

            }) 

        }catch(error){
            console.log('error', error);

        }             
    }

    onMounted(async ()=>{
        await loaddata();
        
    })    

</script>

<template>
    Book List Viewwwwwwwwwwwwwwwwwwwwwwww
    <div>
        <RouterLink :to="{ name: 'book-create' }">Create book</RouterLink>
        <ul>
            <li v-for="(book, index) in bookStore.books">
                {{index}} {{ book.name }} {{ book.author }}

                <RouterLink :to="{name: 'book-edit', params:{id : index}}">
                    <button>Edit</button>
                </RouterLink>
                
                <button @click="bookStore.removeBook(index)">Delete</button>
            </li>
        </ul>
    </div>
</template>