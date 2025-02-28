<template>
    <div class=" bg-[#E8EFEE]">
        <div class="w-full block max-w-7xl mx-auto px-2 py-8 md:px-0 pb-8">
            <motion is="div" preset="slideVisibleBottom" :duration="800" class=" gap-14 bg-[#085c51] p-5 rounded-lg">
                <div class=" flex-col gap-12 flex md:flex-row items-center justify-around">
                    <div class="flex flex-col items-center gap-7 md:gap-12">
                        <div>
                            <h2 class="text-2xl md:text-4xl font-bold text-white  ">Ready to get
                                Started</h2>
                            <p class="text-white font-light text-sm ">Get the app and create
                                your account for free</p>
                        </div>

                        <div class="flex gap-6">
                            <NuxtImg class="w-[7rem] md:w-[11vw]"
                                src="https://scudoapp.co/wp-content/uploads/2023/02/Google-Play-1.svg" />
                            <NuxtImg class="w-[7rem] md:w-[11vw]"
                                src="https://scudoapp.co/wp-content/uploads/2023/02/App-Store-1.svg" />
                        </div>
                    </div>
                    <div class="md:w-[35%] ">
                        <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/scudo-mockup.png" class="w-full" />
                    </div>
                </div>

            </motion>
        </div>

    </div>
</template>

<script setup>

</script>
