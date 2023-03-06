<template>
    <button class="font-bold text-2xl bg-[#FB4747] w-[300px] h-[80px] mt-[10px] hover:bg-[#D00F0F] duration-300 
                    rounded-full border border-[2.5px] border-black" @click="play">
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