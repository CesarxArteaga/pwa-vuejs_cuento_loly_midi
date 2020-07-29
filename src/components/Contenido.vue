<template>
    <div>
        <div class="wrapper">
            <div class="wrapper-picto">
                <div class="tooltip" v-for="p1 in p">
                    <span class="tooltip-content">{{p1.name}}</span>
                    <img class="picto" :src="p1.url" />
                </div>
            </div>
            <div class="wrapper-text">
                 <span v-for="(s,i) in textoarray" v-bind:key="i" :class="classtext">{{s}}</span>
            </div>
           
        </div>
        <button @click.stop="click2">Audio</button>
    </div>
</template>

<script>
import gsap from 'gsap' 

export default {
    name: 'Contenido',
    props: {
        texto:{
            type: String
        }, 
        pictogramas:{
            type: Array
        }
    },
    data(){
        return{
            textoarray:"",
            classtext:"visible", 
            p: []
        }
    },
    mounted(){
        this.textoarray = this.texto.split(" ")
        this.p = this.pictogramas
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
                spans[cont].className = "visible"
                gsap.fromTo(spans[cont],{opacity:0 ,y:-40}, {opacity:1,y: 0, duration: 1.5, ease:'elastic'})
                console.log(cont, this.classtext)     
                cont++
                if(cont===this.textoarray.length){
                    clearInterval(t)
                    this.classtext="visible"
                } 
            },700)
            
            
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

.tooltip-content{
   opacity: 0;
   background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 20px;
  z-index: 1;
}
.tooltip:hover  .tooltip-content{
   opacity: 1;
}

.hide{
  visibility: hidden;
  transition: .1s;
}

.visible{
    visibility: visible;
    transition: .1s;
}
.wrapper{
    height: fit-content;
}
.wrapper-picto{
    width: 100%;
    height: fit-content;
    display: flex;
    align-items: flex-start;
    border: 1px solid black;
}
.picto{
    width: 100px;
}

</style>