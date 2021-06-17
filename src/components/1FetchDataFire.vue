<template>
    <div>
        <h1 v-if="loading">Caricamento in corso...</h1>
        <DataSelect v-if="!loading" :Dati="AllData"/>
    </div>
</template>

<script>
 import DataSelect from "./2DataSelect.vue" 
export default {
    name:"FetchData",
    components:{
        DataSelect
    },
    
    data(){return{
        AllData:[],
        loading:true,
    }},
    created :function(){
         fetch("https://api.npoint.io/9155237c5f3406e1c54d").then(function(fireArray){            
            return fireArray.json()            
        }
        ).then((risp)=>{
            this.AllData=risp;
            this.loading=false;
        }
        );
    },
}
</script>