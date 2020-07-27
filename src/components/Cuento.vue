<template>
    <div>
        <p @click="next">Siguiente</p>
        <p @click="prev">Anterior</p>
        <book class="book"
          :data="pages"
          :turnPageByHand="false"
          ref="book">
      <template slot-scope="prop">
        <img v-if="prop.page.cover" :src="prop.page.urlcover">
        <Contenido :texto="prop.page.title"></Contenido>
      </template>
    </book>
    </div>
</template>

<script>
import Contenido from './Contenido'
import $ from 'jquery'
import book from 'vue-book-component'

export default {
    name: 'Cuento',
    components: {book, Contenido},
    data(){
        return{
            page: 1,
            pages: [
                { cover:true, have_title: false,button: false, urlcover: require('../assets/logo.png'), title: ""},
                { cover:false,have_title: true,button: true,  title: "Argumentos dinámicos de la directiva también funcionan en v-slot, permitiendo la definición de nombres dinámicos en los slots" },
                { cover:true,have_title: true,button: true, urlcover: require('../assets/logo.png'), title: "Para usar un componente con props tienes que importarlo como ya vimos, y en la etiqueta tienes que pasar los props como un atributo más del html" },
                { cover:false,have_title: true,button: true, urlcover: require('../assets/logo.png'), title: "Argumentos dinámicos de la directiva también funcionan en v-slot, permitiendo la definición de nombres dinámicos en los slots" },
                { cover:false,have_title: true,button: true, urlcover: require('../assets/logo.png'), title: "Para usar un componente con props tienes que importarlo como ya vimos, y en la etiqueta tienes que pasar los props como un atributo más del html" },
                { cover:false,have_title: true,button: true, urlcover: require('../assets/logo.png'), title: "Para usar un componente con props tienes que importarlo como ya vimos, y en la etiqueta tienes que pasar los props como un atributo más del html" }
            ]
        }
    }, 
    methods:{    
        next(){
            //this.$refs.book.turn()
            this.$refs.book.next()
            this.$refs.book.resetAnimateClass()
        }, 
        prev(){
            //this.$refs.book.turn(2)
           this.$refs.book.prev()
           this.$refs.book.resetAnimateClass()
        },
    }, 
    mounted: function(){
        
    }
    
}
</script>

<style scoped>
.book{
  position: relative;
  margin: 10% auto 0;
}
.book img{
  width: 100%;
  height: 100%
}

</style>