<template>
    <section class="container">
        <h2>{{title}}</h2>
        <div class="row">
            <div class="col col-6 col-md-4 col-lg-3 mb-3" v-for="(item) in items" :key="item.id">
                <div class="copertina">

                
                <img class="img-copertina" :src="image + item.poster_path" :alt="item.title ? item.title : item.name">

                <div class="overlay">
                    <h3>titolo: {{item.title ? item.title : item.name}}</h3>
                    <h4>titolo originale: {{item.original_titolo ? item.original_titolo : item.original_name}}</h4>
                    <span v-for="(n,index) in 5" :key="index">
                        <i :class="n <=transformScale(item) ? 'fa-solid fa-star golden-star' : 'fa-solid fa-star empty-star'"></i>
                    </span>
                    
                    <img class="flag" 
                        v-if="availableFlags.includes(item.original_language)" 
                        :src="require(`../assets/images/${item.original_language}.png`)" 
                        :alt="`bandiera ${item.original_language}`">
                
                    <p v-else >{{item.original_language}}</p>
                </div>
                
                
            </div>  
            </div>
        </div>
       
        
        <!-- <ul>
            <li v-for="(item) in items" :key="item.id">
                id: {{item.id}}
                titolo originale: {{item.original_titolo ? item.original_titolo : item.original_name}} 
                titolo: {{item.title ? item.title : item.name}}  
                Lingua: {{item.original_language}}
                voto: {{item.vote_average}} 
                
                
            </li>
            
        </ul> -->
         
    </section>
</template>

<script>
// import state from '../store.js'
export default {
    name:'AppGrid',
    props:{
        items: Array,
        loader: Boolean,
        title: String
    },//['items','loader'], 
    data(){
        return{
            image:'https://image.tmdb.org/t/p/w342',
            availableFlags: ['it','en','ja']

        }
    },
    // computed: {
    //     myasearch(){
    //         return state.search
    //     }
    // },
    methods:{
        transformScale(item){
            return parseInt(item.vote_average / 2)
        }
    }
}
</script>

<style lang="scss">
section{
    h2{
        background-color: rgb(153, 2, 2);
        color: white;
    }
    .col{
        

        .copertina{
            position: relative ;
            width: 300px;
            .img-copertina{
                width: 100%;
                display: block;
            }

            .overlay{
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.6);
                color: white;
                opacity: 0;
                &:hover{
                    opacity: 1;
                }
            }
        }
       
    }
    .flag{
        width: 25px;
        display: block;
    }
    
}
.golden-star{
    color: gold;
}
</style>