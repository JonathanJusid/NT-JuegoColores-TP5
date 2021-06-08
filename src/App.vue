<template>
  <div id="app">
    <Header v-bind:adivinarColor="pickedColor" v-bind:colorHeader="colorTitleColor" />
    <Navbar v-bind:mensajeRestart="restartButtonMessage" v-bind:mensaje="message" @reset="resetGame" @cambiarDificultad="changeDifficulty" />
    <Container v-bind:colores="colors" @clickSquare="clickSquare" />
  </div>
</template>

<script>
import Header from './components/header'
import Navbar from './components/navbar'
import Container from './components/container'

export default {
  name: 'App',
  components: {
    Header,
    Navbar,
    Container
  },
  data(){
    return  {
            colorTitleColor: '',
            colorCount: 6,
            isHard: true,
            colors: [],
            pickedColor: '',
            restartButtonMessage: '',
            message: ''
    }
  },
    mounted(){
    this.resetGame();
  },
    methods: {
        resetGame() {
                const colors = this.createNewColors(this.colorCount || 6);
                this.colors = colors;
                this.pickedColor = colors[this.pickColor()];
                this.restartButtonMessage = 'Nuevos colores!';
                this.message = '';
                this.colorTitleColor = '';
        },
        createNewColors(numbers) {
                const arr = [];
                
                for (var i = 0; i < numbers; i++) {
                    arr.push(this.createRandomStringColor());
                }
                return arr;
        },
          pickColor() {
                  const hard = this.isHard ?? true;
                  return Math.floor(Math.random() * (hard ? 6 : 3));
        },    
          createRandomStringColor() {
                  const randomInt = () => Math.floor(Math.random() * 256);
                  return "rgb(" + randomInt() + ", " + randomInt() + ", " + randomInt() + ")";
         },
          changeDifficulty(isHard) {
                      if (this.isHard !== isHard) {
                          this.isHard = isHard;
                          this.colorCount = isHard ? 6 : 3;
                          
                          this.resetGame();
                      }
         }, 
          clickSquare(color, index) {
                    console.log(this.colors, index)
                    if (color === this.pickedColor) {
                    this.message = "Correcto!";
                    this.restartButtonMessage = "Jugá de nuevo";
                            this.colorTitleColor = this.pickedColor;
                        for(const index in this.colors) {
                            this.colors.splice(index, 1, this.pickedColor);
                        }
                    } else {
                              this.colors.splice(index, 1, "#232323");
                      this.message = "Volvé a intentarlo!";
                    }
          },
    }
}
</script>

<style>
#app {
  font-family: "Montserrat", "Avenir";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: #232323;
	margin: 0;	
}
</style>
