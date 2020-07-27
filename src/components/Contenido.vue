<template>
    <div>
        <div class="warpper">
            <span v-for="(s,i) in textoarray" v-bind:key="i" :class="classtext">{{s}}</span>
        </div>
        <button @click="click2">Audio</button>
    </div>
</template>

<script>
import gsap from 'gsap' 
export default {
    name: 'Contenido',
    props: {
        texto:{
            type: String
        }
    },
    data(){
        return{
            textoarray:"",
            classtext:"visible"
        }
    },
    mounted(){
        this.textoarray = this.texto.split(" ")
    },
    methods: {
        click(){
            this.classtext = "hide"
            let cont=0
            let temp = this.textoarray
            if(this.classtext == "hide"){
                this.classtext = "visible"
                this.textoarray = []
                 let t = setInterval(()=>{ 
                    this.textoarray.push(temp[cont])
                    console.log(cont)
                     
                    cont++
                    if(cont===temp.length){
                        clearInterval(t)
                    }
                },400)
            }
        },
        click2(){
            let cont=0
            let spans = this.$el.querySelectorAll('.visible')
            this.classtext='hide'
            let t = setInterval(()=>{
                gsap.fromTo(spans[cont],{opacity:0 ,y:30}, {opacity:1,y: 0, duration: 1.5, ease:'elastic'})
                console.log(cont)     
                cont++
                if(cont===this.textoarray.length){
                    clearInterval(t)
                    this.classtext='visible'
                 }
            },800)
            
        }
    },
    computed:{
        
    }

}
</script>

<style scoped>
.list-item, span {
  display: inline-block;
  margin-right: 10px;
  transition: .2s ease;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}

.hide{
   transition: .1s ;
    opacity: 0;
}
.warpper{
    height: 150px;
}
</style>