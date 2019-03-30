<template>
    <div> 
        <h1 class="alert alert-info">Read a Book</h1><br><br>
        <div class="container">
            <div v-if="readBooks.length > 0" class="row">
                <div v-for="book in readBooks" :key="book.name" class="col-sm-4">
                    <img alt="logo" :src="book.image" style="width:200px;height:200px">
                    <a :href="book.url" :title="book.description">{{book.name}}</a>
                </div>
            </div>
            <div v-else>
                no books
            </div>
        </div>
        
    </div>
</template>

<script>
export default{
    name: 'ReadBook',
    props: ['books'],
    data() {
        return {
            readBooks:[{
            name:'react',
            description:'react for beginner',
            image: require('../assets/react.png'),
            url:'https://reactjs.org/'
            }],
        }
    },
    async mounted() {
        this.books.forEach(book => {
           this.readBooks.push(book) 
        });
    }
}

</script>

<style>


</style>
