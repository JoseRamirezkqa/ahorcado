<template>
    <div class=" flex justify-center animar w-[100%]">
        <div class="fixed  text-center  mt-[30px] z-[100] w-[45%] pt-[8%] h-[700px] duration-300">
            <h1 class="font-bold text-8xl mb-[50px]">
                {{ text }}
            </h1>
            <myButton message="Jugar solo" @play="playSolo" />
            <myButton message="Jugar dos personas" @play="play" />
        </div>
    </div>
</template>
<script>
export default {
    props: {
        text: String,
    },
    methods: {
        playSolo(){
            this.$emit('playSolo');
        },
        play(){
            this.$emit('play');
        }
    }
}
</script>