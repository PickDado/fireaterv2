<template>
    <div>
            <select v-model="Select">
                <option value="">Tutte le date</option>
                <option
                :key="index"
                v-for="(da,index) in SelDin"                
                :value="da"
                >{{da}}
                </option>
            </select>
            <h1>Il numero totale di incendi: {{nOfFidre}}</h1> 
            <FireMap :dati="SelData"/>           
    </div>
    
</template>

<script>

import FireMap from "./3FireMap.vue"
export default {
    name:"DataSelect",
    components:{
        FireMap
    },
    data(){return{
        SelDin:[],
        SelData:[],
        Select:"",
    }},
    props:{
        Dati:Array
    },
    computed:{
        nOfFidre: function(){
            return this.SelData.length
        }
    },

    watch:{
        Select:function(){
            if(this.Select==""){
                this.SelData=this.Dati;
            }else {
                this.SelData=[];
                for(let i = 0;i < this.Dati.length;i++ ){
                if(this.Dati[i].date==this.Select){
                    this.SelData.push(this.Dati[i]);
                    
                }
            }
            }
        }
    },
    
    created: function(){
            this.SelData=this.Dati;
           this.SelDin.push(this.Dati[0].date); 
           for(let i = 0, j = 0 ;i < this.Dati.length;i++ ){
                if(this.SelDin[j]!=this.Dati[i].date){
                    this.SelDin.push(this.Dati[i].date);
                    j++;
                }
            }
            this.SelDin=[...new Set(this.SelDin)];
                     
        },      
}
</script>

<style scoped>
select{
    font-size: x-large;
}
h1{
    font-size: xx-large;
}

</style>