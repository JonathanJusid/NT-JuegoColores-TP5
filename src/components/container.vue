<template>

  <section class="src-componentes-container">
	<div id="container">	
  <Square v-for="(color, index) in colores" v-bind:key="index" v-bind:color="color" @clickSquare="clickSquare(color, index)" />
  
	</div>
  </section>

</template>

<script lang="js">

import Square from './square';


export default  {
    name: 'src-componentes-container',
    props: ['colores'],
    components: {
      Square
  },
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {
      clickSquare(color, index) {
			this.$emit('clickSquare', color, index);
    }
  },
 }
</script>

<style scoped lang="css">
  .src-componentes-container {

  }

#container {
        margin: 20px auto;
        max-width: 600px;
    }

</style>