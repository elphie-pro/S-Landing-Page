<template>
    <div class="bg-[#e8efee]">
        <div class="w-full block max-w-7xl mx-auto px-4 py-8 pb-24">
            <div class=" flex flex-col md:flex-row jusitify-between gap-5 mt-[4rem]">
                <Motion is="div" preset="slideVisibleBottom" :duration="800" class="mt-[5rem]">
                <h2 class="text-[1.8rem] font-bold text-[#085c51]">Simplified <span  class="text-[#fbb040]">Insurance Claim</span> <br class="hidden md:block">Submission</h2> <br>
                <p class="text-sm mt-2 font-light">Filing an insurance claim can be a stressful and time-consuming <br>
                    process, but it doesn't have to be. With our easy insurance claim <br class="hidden md:block">
                    filling system, you can quickly and efficiently submit your claim <br class="hidden md:block">
                    and get on the road to recovery.</p> <br>
                <p class="text-sm mt-2 font-light">Our platform makes it easy to search for and compare Scudo <br class="hidden md:block">
                    streamlines the claim process, allowing you to easily provide all <br class="hidden md:block">
                    necessary information and documentation with just a few clicks. <br class="hidden md:block">
                    No more waiting on hold or struggling to keep track of paper <br class="hidden md:block">
                    forms. Take the hassle out of filing an insurance claim and use <br class="hidden md:block">
                    Scudo to get the support you need.</p>
                    <div class="flex gap-5 mt-10 ">
                        <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/Google-Play-2.svg" class="w-[9rem] md:w-[11vw]"/>
                    <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/App-Store-2.svg" class="w-[9rem] md:w-[11vw]"/>
                    </div>
                    
            </Motion>
            <Motion preset="slideVisibleRight" :duration="800" class="ml-[5%] mt-[3%]">
                <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/scudo-mockup-4.png" class="w-full"/>
            </Motion>
            </div>    
        </div>
        
        
    </div>
</template>

<script setup>

</script>