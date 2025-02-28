<template>
    <div class="bg-[#e8efee] h-[60%] ">
        <div class="w-full block max-w-7xl mx-auto px-4 py-8 pb-24">
            <div class="mt-[5%] flex-col flex md:flex-row jusitify-between gap-[8rem]">
                <Motion is="div" preset="slideVisibleBottom" :duration="800" class="mt-[5%] w-[90%]">
                <h2 class="text-[1.8rem] font-bold text-[#085c51]">Uncover the <span  class=" text-[#fbb040]">Perfect <br class="hidden md:block"> Solution</span> for Your Needs</h2> <br>
                <p class="text-sm font-light">Are you having a tough time finding the right insurance for you <br class="hidden md:block"> and your family? We're here to help!</p> <br>
                <p class="text-sm font-light">Our platform makes it easy to search for and compare different 
                    <br class="hidden md:block"> insurance options, so you can find the coverage that fits your <br class="hidden md:block">
                    specific needs and budget. No more sifting through countless <br class="hidden md:block">
                    policies – simply use our user-friendly interface to discover <br class="hidden md:block">
                    the perfect insurance solution for you. Let us take the stress out of <br class="hidden md:block">
                    finding the right coverage, so you can feel confident and
                    <br class="hidden md:block"> protected.</p>
                    <div class="flex gap-3 md:mt-12 p-5 md:p-0">
                        <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/Google-Play-2.svg" class="w-[8rem] md:w-[11vw]"/>
                    <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/App-Store-2.svg" class="w-[8rem] md:w-[11vw]"/>
                    </div>
                    
            </Motion>
            <Motion preset="slideVisibleRight" :duration="800" class="w-[80%] ">
                <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/scudo-mockup-2.png" class="w-full"/>
            </Motion>
            </div>     
        </div>
       
        
    </div>
</template>

<script setup>

</script>