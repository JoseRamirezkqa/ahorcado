<template>
    <button
        class="bg-[#FB4747] w-[100px] mt-[10px] hover:bg-[#D00F0F] duration-300 rounded-full border border-[2.5px] border-black
        transition ease-in-out delay-150 hover:scale-110" @click="cerrar">
        Cerrar
    </button>
</template>
<script>
export default {
    name: 'buttonCerrar',
    methods:{
        cerrar(){
            this.$emit('cerrar')
        }
    }
}

</script>