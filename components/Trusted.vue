<template>
    <div class="">
        <div class="w-full block max-w-7xl mx-auto px-4">
            <h2 class=" text-2xl mt-3 text-[#FBB040] font-bold">Trusted By</h2>
            <div class=" mt-3 overflow-hidden ">
                <NuxtMarquee :speed="60" :pause-on-hover="true" class="flex items-center ">
                <div v-for="company in trustCompanies">
                    <NuxtImg :src="company.logo" class="w-[9rem] md:w-[12rem] ml-20 "/>
                </div>
            </NuxtMarquee>
            </div>   
        </div>
        
    </div>
</template>

<script setup>
    const trustCompanies = [
        {
            name: 'Conernerstone',
            logo: 'https://scudoapp.co/wp-content/uploads/2023/02/cornerstone.png'
        },
        {
            name:'Custodian',
            logo: 'https://scudoapp.co/wp-content/uploads/2023/02/custodian.png'
        },
        {
            name:'Leadway Insurance',
            logo: 'https://scudoapp.co/wp-content/uploads/2023/02/leadway.png'
        },
        {
            name:'Mansard',
            logo: 'https://scudoapp.co/wp-content/uploads/2023/02/axa-mansard.png'
        }
    ]
</script>

