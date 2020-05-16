<template>
<div id="app">
    <div>
        <h1 class="headline">Recipies: </h1>
        <div v-for="item in content" :key="item">
            <div class="wrap">
                <h1>{{item.title}}</h1>
                <img :src="item.thumbnail">
                <p><span>Ingredients:</span> {{item.ingredients}}</p>
                <a :href="item.href">Link to recipe</a>
            </div>
        </div>
    </div>
    
</div>
</template>

<script>
    
    export default {
        data() {
    return {
        content: []
    }
},
    beforeMount() {
        const app = this;
        
        const conversionUrl = "https://cors-anywhere.herokuapp.com/"
        const url = "http://www.recipepuppy.com/api/"

        fetch(conversionUrl + url)
        .then(function(response) {
            return response.json();
        })
        .then(function(result) {
            app.content = result.results;
            
        })
        .catch(function(error) {
            console.log("error", error)
        })
        
    }
}
</script>

<style>
    body {
        background-color: black;
        margin: 0;
        padding: 0;
    }
    .headline{
        color: white;
        font-size: 40px;
        margin: 20px;
    }
    .wrap{
        border: 1px solid black;
        margin: 20px;
        padding: 20px;
        max-width: 40vh;
        background-color: white;
        border-radius: 30px;
    }

    p{
        font-weight: bold;
    }
    span{
        font-size: 20px;
    }
    img:hover{
        width: 100%;
        cursor: pointer;
    }
    a{
        text-decoration: none;
        border: 1px solid black;
        padding: 5px;
        background-color: green;
        color: white;
        
    }
    a:hover{
        background-color: darkgreen;
        
    }
    a:active{
        opacity: 0.5;
    }
</style>
