<template>
    <button class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-500 
                    rounded-full border mr-[10px] border-[2.5px] border-black transition ease-in-out delay-150 hover:scale-110" @click="play">
        {{ message }}
    </button>
</template>
<script>
export default {
    name: 'myButton',
    props: {
        message: {
            type: String,
            required: true,
        }
    },
    methods:{
        play(){
            this.$emit('play')
        }
    }
}
</script>