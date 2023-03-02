<template>
  <div>

    <div class=" flex justify-center animar w-[100%]" :class="{ hidden: active }">
      <div class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300">
        <h1 class="text-2xl mt-[5px] font-bold">Debe ingresar una palabra</h1>
        <button v-on:click="cambia" class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                          rounded-full border border-[2.5px] border-black">
          Cerrar
        </button>
      </div>
    </div>
    <div class=" flex justify-center animar w-[100%]" :class="{ hidden: activeLetra }">
      <div class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300">
        <h1 class="text-2xl mt-[5px] font-bold">El campo está Vacio</h1>
        <button v-on:click="cambiaDos" class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                                            rounded-full border border-[2.5px] border-black">
          Cerrar
        </button>
      </div>
    </div>
    <div v-if="!incio">
      <input type="text" v-model="palabra" v-on:keyup.enter="save" placeholder="Ingrese la palabra"
        class="border-2 m-[2rem]" autofocus ref="inputPalabra">
    </div>
    <div v-else-if="incio && !win && !lose">
      <input type="text" v-model="letra" v-on:keyup.enter="comprobar" placeholder="digite una letra"
        class="border-2 m-[2rem]" autofocus maxlength="1" ref="inputLetra">
      <div id="arregloDivs" class="mx-[2rem] flex">
        <div v-for="el in arrayPalabra" class="border-2 w-[50px] h-[50px]  text-center" :ref="el">
        </div>
      </div>
    </div>
    <div class=" flex justify-center animar w-[100%]">
      <div v-if="win"
        class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300">
        <h1 class="text-2xl mt-[5px] font-bold">¡Ha ganado!</h1>
      </div>
    </div>
    <div class=" flex justify-center animar w-[100%]">
      <div v-if="lose"
        class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300">
        <h1 class="text-2xl mt-[5px] font-bold">Perdió</h1>
      </div>
    </div>
    <canvas class=" bg-gray-100" ref="lienzo" v-show="incio && !win && !lose">
    </canvas>
  </div>
</template>
<script>
export default {
  data() {
    return {
      incio: false,
      win: false,
      lose: false,
      palabra: '',
      letra: '',
      arrayPalabra: [],
      arrayComprobar: [],
      aciertos: 0,
      errores: 0,
      active: true,
      activeLetra: true,
    }
  },
  methods: {
    save() {
      if (this.palabra != "") {
        this.incio = true;
        this.arrayPalabra = Array.from(this.palabra);
        this.arrayComprobar = Array.from(this.palabra);
        console.log(this.arrayPalabra)
        console.log(this.arrayComprobar)
        this.palabra = ''
        this.dibujar()
      } else {
        this.active = false;
        this.$refs.inputPalabra.disabled = true;
      }
    },
    comprobar() {
      if (this.letra != "" && this.letra.length == 1) {
        if (this.arrayComprobar.indexOf(this.letra) != -1) {
          this.aciertos += 1
          this.$refs[this.letra][0].textContent = this.letra
          console.log(this.arrayComprobar.indexOf(this.letra))
          this.arrayComprobar.splice(this.arrayComprobar.indexOf(this.letra), 1)
          console.log(this.arrayComprobar)
          this.letra = ""
        } else {
          this.letra = ""
          this.errores += 1;
        }
        if (this.aciertos == this.arrayPalabra.length) {
          this.win = true;
        }
        this.dibujar()

      } else if (this.letra == "") {
        this.activeLetra = false;
        this.$refs.inputLetra.disabled = true;

      }
    },
    dibujar() {
      this.$refs.lienzo.width = 800;
      this.$refs.lienzo.height = 800;
      console.log(this.$refs.lienzo)
      const dibujo = this.$refs.lienzo.getContext('2d');
      dibujo.beginPath();
      dibujo.moveTo(700, 700);
      dibujo.lineTo(100, 700);
      dibujo.moveTo(200, 700);
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
        dibujo.lineTo(500, 550);
        dibujo.stroke();
      } else if (this.errores == 3) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 550);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(425, 425)
        dibujo.stroke();
      } else if (this.errores == 4) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 550);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(425, 425);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(575, 425)
        dibujo.stroke();
      } else if (this.errores == 5) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 550);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(425, 425);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(575, 425);
        dibujo.moveTo(500, 550);
        dibujo.lineTo(425, 600)
        dibujo.stroke();
      } else if (this.errores == 6) {
        dibujo.moveTo(550, 250);
        dibujo.arc(500, 250, 50, 0, 2 * Math.PI)
        dibujo.stroke();
        dibujo.moveTo(500, 300);
        dibujo.lineTo(500, 550);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(425, 425);
        dibujo.moveTo(500, 375);
        dibujo.lineTo(575, 425);
        dibujo.moveTo(500, 550);
        dibujo.lineTo(425, 600);
        dibujo.moveTo(500, 550);
        dibujo.lineTo(575, 600)
        dibujo.stroke();
      } else if (this.errores >= 7) {
        this.lose = true;
      }
    },
    cambia() {
      this.active = true;
      this.$refs.inputPalabra.disabled = false;
    },
    cambiaDos() {
      this.activeLetra = true;
      this.$refs.inputLetra.disabled = false;

    }
  }
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
</style>