<template>
  <div v-on:click="dibujar">
    <div v-if="!incio">
      <input type="text" v-model="palabra" v-on:keyup.enter="save" placeholder="Ingrese la palabra"
        class="border-2 m-[2rem]" autofocus>
    </div>
    <div v-else-if="incio && !win">
      <input type="text" v-model="letra" v-on:keyup.enter="comprobar" placeholder="digite una letra"
        class="border-2 m-[2rem]" autofocus>
      <div id="arregloDivs" class="mx-[2rem]">
        <div v-for="(el, index) in arrayPalabra" class="border-2 w-[50px] h-[50px] inline-block text-center" :ref="el">
          {{ index }}
        </div>
      </div>
    </div>
    <div v-if="win">
      <h1>¡Ha ganado!</h1>
    </div>
      <canvas class=" bg-gray-100" ref="lienzo">
      </canvas>
  </div>
</template>
<script>
export default {
  data() {
    return {
      incio: false,
      win: false,
      palabra: '',
      letra: '',
      arrayPalabra: [],
      aciertos: 0,
      errores: 0
    }
  },
  methods: {
    save() {
      this.incio = true;
      this.arrayPalabra = Array.from(this.palabra);
      this.palabra = ''
    },
    comprobar() {
      if (this.arrayPalabra.indexOf(this.letra) != -1) {
        this.aciertos += 1
        console.log(this.aciertos);
        if (this.aciertos == this.arrayPalabra.length) {
          this.win = true;
        }
        alert('existe')
        this.$refs[this.letra][0].textContent = this.letra
        this.letra = ""
      } else {
        alert('no existe')
        this.letra = ""
      }
    },
    dibujar() {
      alert('entró')
      console.log(this.$refs.lienzo)
      this.$refs.lienzo.width = 800;
      this.$refs.lienzo.height = 800;
      const dibujo = this.$refs.lienzo.getContext('2d');
      dibujo.beginPath();
      dibujo.moveTo(0,0);
      dibujo.lineTo(50,50);
      dibujo.stroke();

    }
  }
}

</script>