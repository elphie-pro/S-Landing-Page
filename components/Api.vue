<template>
    <div class="">
        <div class="w-full block max-w-7xl mx-auto px-4 py-8 pb-24">
            <Motion is="div" preset="slideVisibleBottom" :duration="800">
                <div class="flex flex-col">
                  <div class="text-center ">
                    <h2 class="text-[1.8rem] font-bold text-[#085c51]">Get the insurance tech <span class="text-[#fbb040]">API</span> you need for <br> your next project from Scudo!</h2> 
                    <p class="font-light text-sm mt-7">Get started with our easy-to-use developer documentation and test out our
                        <br>app on our development environment before production.</p>  
                    </div>         
                    <div class="flex flex-col md:flex-row gap-5 items-center md:ml-[27rem] mt-10">
                        <button class="w-[20rem] md:w-[10rem] h-[6vh] border rounded-lg bg-[#0d542b] text-white">Request Access</button>
                        <button class="w-[20rem] md:w-[13rem] h-[6vh] bg-white border rounded-lg border-[#085c51] text-[#085c51]">View Documentation</button>
                    </div>     
                    <div class="jusitfy-center mt-8 flex items-center">
                        <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/code-mockup-1536x1026.png" class="w-full"/>
                    </div> 
                </div>
                
            </Motion>            
        </div>

    </div>
</template>

<script setup>

</script>

