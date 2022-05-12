<template>
    <section>
        <h2>{{title}}</h2>
        <ul>
            <li v-for="(item) in items" :key="item.id">
                id: {{item.id}}
                titolo originale: {{item.original_titolo ? item.original_titolo : item.original_name}} <!-- {{item.original_titolo ? item.original_titolo : item.original_name}}-->
                titolo: {{item.title ? item.title : item.name}}  <!-- {{item.title ? item.title : item.name}}-->
                Lingua: {{item.original_language}} <!-- <img :src="require('./assets/images/'+item.original_language+'.jpg')" :alt="item.original_language"> -->
                voto: {{item.vote_average}} 
            </li>
        </ul>
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
            
        }
    },
    // computed: {
    //     myasearch(){
    //         return state.search
    //     }
    // },
    methods:{
       
    }
}
</script>

<style lang="scss">

</style>