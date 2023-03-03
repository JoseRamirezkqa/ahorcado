<template>
  <div>
    <div class="text-center">
      <h1 class="font-bold text-6xl mt-[10px] mb-[30px]">Ahorcado</h1>
    </div>
    <!-- modales-->
    <div class=" flex justify-center animar w-[100%] " :class="{ hidden: active }">
      <div class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300 bg-white">
        <h1 class="text-2xl mt-[5px] font-bold">Debe ingresar una palabra</h1>
        <button v-on:click="cambia" class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                    rounded-full border border-[2.5px] border-black">
          Cerrar
        </button>
      </div>
    </div>
    <div class=" flex justify-center animar w-[100%]" :class="{ hidden: activeLetra }">
      <div
        class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300 bg-white">
        <h1 class="text-2xl mt-[5px] font-bold">El campo está Vacio</h1>
        <button v-on:click="cambiaDos" class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                     rounded-full border border-[2.5px] border-black">
          Cerrar
        </button>
      </div>
    </div>
    <div class=" flex justify-center animar w-[100%]" :class="{ hidden: activeLetraRepetida }">
      <div
        class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300 bg-white">
        <h1 class="text-2xl mt-[5px] font-bold">No se puede ingresar la misma letra dos veces</h1>
        <button v-on:click="cambiaTres" class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                      rounded-full border border-[2.5px] border-black">
          Cerrar
        </button>
      </div>
    </div>
    <!-- juego -->
    <div class="border border-2 border-black w-[50%] h-[800px] m-auto text-center" :class="{ per: activeBg }">
      <div v-if="!start" class="my-[15%]">
        <h1 class="font-bold text-8xl mb-[50px]">
          Eliga el modo de juego
        </h1>
        <button v-on:click="playSolo" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                    rounded-full border border-[2.5px] border-black">
          Jugar solo
        </button>
        <button v-on:click="play" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                rounded-full border border-[2.5px] border-black">
          Jugar dos personas
        </button>
      </div>
      <div v-if="!incio && start" class="h-[100%] p-[10%] bg-gray-200">
        <h1 class="font-bold text-6xl ">
          Para empezar el juego Ingrese la palabra el jugador que no va a adivinar
        </h1>
        <input type="text" v-model="palabra" v-on:keyup.enter="save" placeholder="Ingrese la palabra"
          class="border-2 m-[2rem] border-black w-[300px]" autofocus ref="inputPalabra">
      </div>
      <div v-else-if="incio && !win && !lose">
        <input type="text" v-model="letra" v-on:keyup.enter="comprobar" placeholder="digite una letra"
          class="border-2 mt-[30px] mb-[20px] border-black" autofocus maxlength="1" ref="inputLetra">
        <div id="arregloDivs" class="mx-[2rem] flex justify-center mb-[30px]">
          <div v-for="el in arrayPalabra" class="border-2 border-black w-[50px] h-[50px]  text-center font-bold"
            :ref="el">
          </div>
        </div>
      </div>
      <div class=" flex justify-center animar w-[100%]">
        <div v-if="win" class="fixed  text-center  mt-[30px] z-[100] w-[45%] pt-[8%] h-[700px] duration-300">
          <h1 class="font-bold text-8xl mb-[50px]">
            Ganó, felicitaciones
          </h1>
          <button v-on:click="playSolo" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                    rounded-full border border-[2.5px] border-black">
            Jugar solo
          </button>
          <button v-on:click="play" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                rounded-full border border-[2.5px] border-black">
            Jugar dos personas
          </button>
        </div>
      </div>
      <div class=" flex justify-center animar w-[100%]">
        <div v-if="lose" class="fixed  text-center  mt-[30px] z-[100] w-[45%] pt-[8%] h-[700px] duration-300">
          <h1 class="font-bold text-8xl mb-[50px]">
            Perdió, Vuelve a intertarlo
          </h1>
          <button v-on:click="playSolo" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                    rounded-full border border-[2.5px] border-black">
            Jugar solo
          </button>
          <button v-on:click="play" class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                                rounded-full border border-[2.5px] border-black">
            Jugar dos personas
          </button>
        </div>
      </div>
      <canvas class=" bg-gray-100 m-auto" ref="lienzo" v-show="incio && !win && !lose">
      </canvas>
    </div>
    <myButton/> 
  </div>
</template>
<script>
import { data } from '../data/palabras.js';
import myButton from '../components/button.vue'
export default {
  components:{
    myButton
  },
  data() {
    return {
      incio: false,
      win: false,
      lose: false,
      start: false,
      palabra: '',
      letra: '',
      arrayPalabra: [],
      arrayComprobar: [],
      arrayLetras: [],
      aciertos: 0,
      errores: 0,
      active: true,
      activeLetra: true,
      activeLetraRepetida: true,
      activeBg: false,
      contador: 0,
    }
  },
  mounted() {
    console.log(data);
  },
  methods: {
    save() {
      console.log(data)
      if (this.palabra != "") {
        this.incio = true;
        this.arrayPalabra = Array.from(this.palabra);
        this.arrayComprobar = Array.from(this.palabra);
        this.palabra = ''
        this.dibujar()
      } else {
        this.active = false;
        this.$refs.inputPalabra.disabled = true;
        this.activeBg = true;
      }
    },
    comprobar() {
      if (this.letra != "" && this.letra.length == 1) {
        if (this.arrayLetras.indexOf(this.letra) == -1) {
          this.arrayLetras.push(this.letra);
          if (this.arrayComprobar.indexOf(this.letra) != -1) {
            for (let i = 0; i < this.arrayPalabra.length; i++) {
              if (this.arrayPalabra[i] == this.letra) {
                this.aciertos += 1
                this.$refs[this.letra][0].textContent = this.letra
                if (this.contador >= 1) {
                  this.$refs[this.letra][this.contador].textContent = this.letra
                  this.arrayComprobar.splice(this.arrayComprobar.indexOf(this.letra, this.contador), 1)
                }
                this.contador += 1
              }
            }
            this.arrayComprobar.splice(this.arrayComprobar.indexOf(this.letra), 1)
            this.contador = 0
            this.letra = ""
          } else {
            this.letra = ""
            this.errores += 1;
          }
          if (this.aciertos == this.arrayPalabra.length) {
            this.win = true;
          }
          this.dibujar()
        } else if (this.arrayLetras.indexOf(this.letra) != -1) {
          this.activeLetraRepetida = false;
          this.$refs.inputLetra.disabled = true;
          this.activeBg = true;
          this.letra = ""
        }
      } else if (this.letra == "") {
        this.activeLetra = false;
        this.$refs.inputLetra.disabled = true;
        this.activeBg = true

      }
    },
    dibujar() {
      this.$refs.lienzo.width = 800;
      this.$refs.lienzo.height = 600;
      const dibujo = this.$refs.lienzo.getContext('2d');
      dibujo.beginPath();
      dibujo.moveTo(700, 550);
      dibujo.lineTo(100, 550);
      dibujo.moveTo(200, 550);
      dibujo.lineTo(200, 100);
      dibujo.lineTo(500, 100);
      dibujo.lineTo(500, 200);
      dibujo.stroke();
      if (this.errores == 1) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
      } else if (this.errores == 2) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 450);
        dibujo.stroke();
      } else if (this.errores == 3) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 450);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(425, 400)
        dibujo.stroke();
      } else if (this.errores == 4) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 450);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(425, 400);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(575, 400)
        dibujo.stroke();
      } else if (this.errores == 5) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 450);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(425, 400);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(575, 400);
        dibujo.moveTo(500, 450);
        dibujo.lineTo(425, 500)
        dibujo.stroke();
      } else if (this.errores == 6) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 450);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(425, 400);
        dibujo.moveTo(500, 350);
        dibujo.lineTo(575, 400);
        dibujo.moveTo(500, 450);
        dibujo.lineTo(425, 500);
        dibujo.moveTo(500, 450);
        dibujo.lineTo(575, 500)
        dibujo.stroke();
      } else if (this.errores >= 7) {
        this.lose = true;
      }
    },
    cambia() {
      this.active = true;
      this.$refs.inputPalabra.disabled = false;
      this.activeBg = false;
    },
    cambiaDos() {
      this.activeLetra = true;
      this.$refs.inputLetra.disabled = false;
      this.activeBg = false;
    },
    cambiaTres() {
      this.activeLetraRepetida = true;
      this.$refs.inputLetra.disabled = false;
      this.activeBg = false;
    },
    play() {
      this.incio = false
      this.win = false
      this.lose = false
      this.start = true
      this.palabra = ''
      this.letra = ''
      this.arrayPalabra = []
      this.arrayComprobar = []
      this.arrayLetras = []
      this.aciertos = 0
      this.errores = 0
      this.active = true
      this.activeLetra = true
      this.activeLetraRepetida = true
      this.activeBg = false
      this.contador = 0
    },
    playSolo() {
      this.incio = true
      this.win = false
      this.lose = false
      this.start = true
      this.palabra = ''
      this.letra = ''
      this.arrayPalabra = []
      this.arrayComprobar = []
      this.arrayLetras = []
      this.aciertos = 0
      this.errores = 0
      this.active = true
      this.activeLetra = true
      this.activeLetraRepetida = true
      this.activeBg = false
      this.contador = 0
      this.palabra = removeAccents(data[parseInt(Math.random() * 5000)])
      console.log(this.palabra)
      this.save()
    }
  }
}
const removeAccents = (str) => {
  return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
} 
</script>
<style>
.animar {
  -webkit-animation-name: animarsuperior;
  -webkit-animation-duration: 0.5s;
  animation-name: animarsuperior;
  animation-duration: 0.5s;
}


@keyframes animarsuperior {
  from {
    top: -300px;
    opacity: 0
  }

  to {
    top: 0;
    opacity: 1
  }
}

.per {
  background-color: rgb(165, 165, 165);
  opacity: .2;
}
</style>