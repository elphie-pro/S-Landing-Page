<template>
    <div class=" bg-[#f8fffe]">
        <div class="-mt-[7rem]">
            <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/frame-1-bg.png" class="w-[4rem] mt-[8rem]" />
        </div>
        <div class="w-full block max-w-6xl mx-auto px-4  pb-24">
            <div class="flex-col flex md:flex-row items-center gap-[8rem]">
                <Motion preset="slideVisibleLeft" :duration="800" class="w-[110%]">
                    <NuxtImg src="https://scudoapp.co/wp-content/uploads/2023/02/scudo-mockup-1.png"
                        class="w-full" />
                </Motion>
                <Motion is="div" preset="slideVisibleBottom" :duration="800" class="">
                    <h2 class="text-[1.8rem] font-bold text-[#085c51]">Scudo is here to help you <br
                            class="hidden md:block"> <span class="text-[#fbb040]">safeguard</span> your future</h2>
                    <p class="text-sm">Don't wait to secure your future – choose from Scudo's top <br
                            class="hidden md:block"> insurance products from leading companies and get protected <br
                            class="hidden md:block"> now. Start your coverage today!</p>
                    <ul class="space-y-8 md:space-y-12 ">
                        <li v-for="safe in SafeGuard" class="flex gap-3 mt-5 md:gap-4 items-start w-[90%]">
                            <div v-html="safe.icon" :class="safe.iconColor"
                                class="shrink-0 p-2 rounded-lg text-white" />
                            <div class="flex flex-col gap-2">
                                <h2 class="text-[#085c51] font-bold text-xl">{{ safe.title }}</h2>
                                <p class="text-sm text-justify">{{ safe.text }}</p>
                            </div>
                        </li>
                    </ul>
                </Motion>
            </div>
        </div>
    </div>
</template>

<script setup>
const SafeGuard = [
    {
        title: "Uncover the Perfect Insurance Solution for Your Needs",
        text: "Scudo helps you easily find and compare insurance options to discover the perfect solution for your needs.",
        iconColor: "bg-[#085c51]",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="m7.875 14.25 1.214 1.942a2.25 2.25 0 0 0 1.908 1.058h2.006c.776 0 1.497-.4 1.908-1.058l1.214-1.942M2.41 9h4.636a2.25 2.25 0 0 1 1.872 1.002l.164.246a2.25 2.25 0 0 0 1.872 1.002h2.092a2.25 2.25 0 0 0 1.872-1.002l.164-.246A2.25 2.25 0 0 1 16.954 9h4.636M2.41 9a2.25 2.25 0 0 0-.16.832V12a2.25 2.25 0 0 0 2.25 2.25h15A2.25 2.25 0 0 0 21.75 12V9.832c0-.287-.055-.57-.16-.832M2.41 9a2.25 2.25 0 0 1 .382-.632l3.285-3.832a2.25 2.25 0 0 1 1.708-.786h8.43c.657 0 1.281.287 1.709.786l3.284 3.832c.163.19.291.404.382.632M4.5 20.25h15A2.25 2.25 0 0 0 21.75 18v-2.625c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125V18a2.25 2.25 0 0 0 2.25 2.25Z" />
</svg>
`
    },
    {
        title: "Simplified Insurance Claim Submission",
        text: "Scudo's insurance claim filling system simplifies the process and allows for quick and efficient submission of claims with just a few clicks. No more stress or hassle.",
        iconColor: "bg-[#fbb040]",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6">
  <path fill-rule="evenodd" d="M2.625 6.75a1.125 1.125 0 1 1 2.25 0 1.125 1.125 0 0 1-2.25 0Zm4.875 0A.75.75 0 0 1 8.25 6h12a.75.75 0 0 1 0 1.5h-12a.75.75 0 0 1-.75-.75ZM2.625 12a1.125 1.125 0 1 1 2.25 0 1.125 1.125 0 0 1-2.25 0ZM7.5 12a.75.75 0 0 1 .75-.75h12a.75.75 0 0 1 0 1.5h-12A.75.75 0 0 1 7.5 12Zm-4.875 5.25a1.125 1.125 0 1 1 2.25 0 1.125 1.125 0 0 1-2.25 0Zm4.875 0a.75.75 0 0 1 .75-.75h12a.75.75 0 0 1 0 1.5h-12a.75.75 0 0 1-.75-.75Z" clip-rule="evenodd" />
</svg>
`
    },
    {
        title: "1:1 Direct Messaging",
        text: "Easily communicate with insurance providers through chat with our platform's real-time feature. No more waiting on hold or phone navigation.",
        iconColor: "bg-green-400",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6">
  <path fill-rule="evenodd" d="M4.804 21.644A6.707 6.707 0 0 0 6 21.75a6.721 6.721 0 0 0 3.583-1.029c.774.182 1.584.279 2.417.279 5.322 0 9.75-3.97 9.75-9 0-5.03-4.428-9-9.75-9s-9.75 3.97-9.75 9c0 2.409 1.025 4.587 2.674 6.192.232.226.277.428.254.543a3.73 3.73 0 0 1-.814 1.686.75.75 0 0 0 .44 1.223ZM8.25 10.875a1.125 1.125 0 1 0 0 2.25 1.125 1.125 0 0 0 0-2.25ZM10.875 12a1.125 1.125 0 1 1 2.25 0 1.125 1.125 0 0 1-2.25 0Zm4.875-1.125a1.125 1.125 0 1 0 0 2.25 1.125 1.125 0 0 0 0-2.25Z" clip-rule="evenodd" />
</svg>
`
    }
]
</script>
