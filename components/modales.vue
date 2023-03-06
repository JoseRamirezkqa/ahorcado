<template>
    <div class=" flex justify-center animar w-[100%] " >
        <div class="fixed border text-center border-2 border-black mt-[30px] z-[100] w-[30%] h-[100px] duration-300 bg-white">
            <h1 class="text-2xl mt-[5px] font-bold">
                {{text}} 
            </h1>
            <buttonCerrar @cerrar="cambia" />
        </div>
    </div>
</template>
<script>
    export default{
        props:{
            text:{
                type: String
            }
        },
        methods:{
            cambia(){
                this.$emit('cambia')
            },
        }
    }
</script>