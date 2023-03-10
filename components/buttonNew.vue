<template>
    <button
        class=" w-[200px] mt-[10px] hover:bg-[#9F9C9C] duration-500 rounded-full border border-[2.5px] border-black
        transition ease-in-out delay-150 hover:scale-110" @click="cerrar">
        {{text}}
    </button>
</template>
<script>
export default {
    name: 'buttonCerrar',
    props: {
        text: String,
    },
    methods:{
        cerrar(){
            this.$emit('cerrar')
        }
    }
}

</script>