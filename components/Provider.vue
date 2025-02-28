<template>
    <div class="bg-[#f8fffe] ">
     <div>
        <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/frame-1-bg.png" class="w-[3rem] mt-[0rem] "/>    
    </div>
    <div class="w-full block max-w-7xl mx-auto px-4 pb-24">
        <div class="">
            <div class="mt-[1.5%] flex flex-col md:flex-row jusitify-between gap-5">
            <Motion preset="slideVisibleLeft" :duration="800" class="">
                <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/scudo-mockup-3.png" class="w-full"/>
            </Motion>
            <div class="">
                <Motion is="div" preset="slideVisibleBottom" :duration="800" class="mt-[8%]">
                    <h2 class="text-[1.6rem] font-bold text-[#085c51]">Chat with <span class="text-[#fbb040]">Insurance <br> Provider</span></h2> <br>
                    <p class="text-sm mt-5 font-light">Communicating with insurance providers doesn't have to be a <br class="hidden md:block">
                        hassle. With our platform, you can now easily chat with insurance <br class="hidden md:block">
                        companies in real time. No more waiting on hold or trying to <br class="hidden md:block">
                        navigate automated phone systems – simply log in to our <br class="hidden md:block">
                        platform and select the provider you want to connect with. <br class="hidden md:block">
                        Whether you have questions about a policy or need to clarify <br class="hidden md:block">
                        details, our chat feature makes it easy to get the information you <br class="hidden md:block">
                        need.</p> <br>
                    <p class="text-sm  font-light">Experience the convenience and simplicity of Scudo and <br> start chatting with insurance companies today.</p>
                </Motion>    
            </div>
            
            </div>    
    </div>
   
    </div>   
    </div>
    
</template>

<script setup>

</script>
