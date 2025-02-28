<template>
    <div class=" bg-[#085c51]">
      <div class="w-full block max-w-7xl mx-auto px-4 md:px-0 py-8 pb-8">
        <div class="flex flex-col md:flex-row gap-10">
            <div class="flex flex-col gap-5 ml-[3rem] text-white">
                <h2 class="font-semibold ">Quicklinks</h2>
                <ul class="font-extralight ">
                    <li class="hover:underline">About</li>
                    <li class="hover:underline">Blog</li>
                    <li class="hover:underline">API</li>
                    <li class="hover:underline">Contact Us</li>
                </ul>
            </div>
            <div class="flex flex-col gap-5 md:ml-[10%] ml-[3rem] text-white">
                <h2 class="font-semibold ">Products</h2>
                <ul class="font-extralight ">
                    <li class="hover:underline">Sudo Mobile App(IOS)</li>
                    <li class="hover:underline">Sudo Mobile App(Andrios)</li>
                    <li class="hover:underline">Sudo Insurance System</li>
                </ul>
            </div>
            <div class="flex flex-col gap-5 md:ml-[7%] ml-[3rem] text-white">
                <h2 class="font-semibold ">Legal</h2>
                <ul class="font-extralight ">
                    <li class="hover:underline">Privacy Policy</li>
                    <li class="hover:underline">Cookies Policy</li>
                    <li class="hover:underline">Terms and Conditions</li>
                </ul>
            </div>
            <div class="flex flex-col gap-5 ml-[3rem] text-white">
                <h2 class="font-semibold ">Get A Newsletter</h2>
                <p class="font-light text-[.8rem]">For the latest deals and tips, subscribe <br>to our newsletter</p>
                <div class="flex flex-col md:flex-row">
                    <input type="text" placeholder="Email Address" class="w-[15rem] md:w-[10rem] h-[2.5rem] bg-transparent border rounded-t-md md:rounded-tr-none md:rounded-l-md p-2">
                    <button class="w-[15rem] md:w-[4rem] h-[2.5rem]  bg-white text-[#085c51] border rounded-b-md md:rounded-b-none md:rounded-r-md">Join</button>    
                </div>
                <div class="flex space-x-4 mt-1 ml-1">
            <!-- Example using Heroicons (or FontAwesome) -->
            <a href="#" class="hover:opacity-75 transition">
              <!-- Facebook Icon -->
              <svg
                class="h-6 w-6"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M22.675 0H1.325C.594 0 0 .594 0 1.326v21.348C0 23.406.594 24 1.325 24h11.495v-9.294H9.847v-3.622h2.973V8.413c0-2.945 1.796-4.551 4.415-4.551 1.255 0 2.337.093 2.648.135v3.07l-1.818.001c-1.426 0-1.701.678-1.701 1.67v2.188h3.403l-.443 3.622h-2.96V24h5.797c.73 0 1.324-.594 1.324-1.326V1.326C24 .594 23.406 0 22.675 0z"
                />
              </svg>
            </a>
            <a href="#" class="hover:opacity-75 transition">
              <!-- Twitter Icon -->
              <svg
                class="h-6 w-6"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M23.954 4.569c-.885.389-1.83.654-2.825.775 
                  1.014-.611 1.794-1.574 2.163-2.724-.951.555-2.005.959-3.127 
                  1.184-.897-.959-2.178-1.555-3.594-1.555-2.72 0-4.924 
                  2.204-4.924 4.917 0 .39.045.765.127 1.124-4.09-.205-7.72-2.165-10.148-5.144-.424.722-.666 
                  1.561-.666 2.475 0 1.71.87 3.213 2.188 4.096-.807-.026-1.566-.248-2.228-.616v.06c0 
                  2.385 1.693 4.374 3.946 4.827-.413.111-.849.171-1.296.171-.314 0-.624-.03-.927-.086.631 
                  1.953 2.445 3.376 4.6 3.416-1.68 1.319-3.809 2.107-6.115 
                  2.107-.398 0-.79-.023-1.175-.068 2.179 1.394 4.768 2.209 
                  7.557 2.209 9.054 0 14.002-7.496 14.002-13.986 0-.21 
                  0-.42-.015-.63.961-.689 1.8-1.56 2.46-2.548l-.047-.02z"
                />
              </svg>
            </a>
            <a href="#" class="hover:opacity-75 transition">
              <!-- Instagram Icon -->
              <svg
                class="h-6 w-6"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M12 2.163c3.204 0 3.584.012 4.85.07 
                  3.252.148 4.771 1.691 4.919 4.919.058 
                  1.266.069 1.646.069 4.849 0 3.204-.012 
                  3.584-.069 4.85-.148 3.225-1.664 4.771-4.919 
                  4.919-1.266.058-1.646.069-4.85.069-3.204 
                  0-3.584-.012-4.85-.069-3.255-.148-4.771-1.694-4.919-4.919C2.175 
                  15.615 2.163 15.235 2.163 12c0-3.203.012-3.583.07-4.849.148-3.225 
                  1.664-4.771 4.919-4.919C8.416 2.175 8.796 2.163 12 
                  2.163zm0 1.84c-3.17 0-3.552.012-4.795.069-2.641.12-3.86 
                  1.316-3.98 3.98-.057 1.243-.068 1.624-.068 
                  4.794s.011 3.552.068 4.795c.12 2.664 1.338 3.86 
                  3.98 3.98 1.243.057 1.624.068 4.795.068s3.552-.011 
                  4.795-.068c2.64-.12 3.86-1.316 3.98-3.98.057-1.243.068-1.624.068-4.795s-.011-3.552-.068-4.795c-.12-2.64-1.338-3.86-3.98-3.98-1.243-.057-1.624-.068-4.795-.068zm0 
                  4.738a5.259 5.259 0 1 1 0 10.518 5.259 
                  5.259 0 0 1 0-10.518zm0 8.678a3.419 3.419 
                  0 1 0 0-6.838 3.419 3.419 0 0 0 0 6.838zm4.271-8.845a1.221 
                  1.221 0 1 1 2.442 0 1.221 1.221 0 0 1-2.442 0z"
                />
              </svg>
            </a>
          </div>

            </div>
        </div>
        <div class="mt-20 pt-4 text-center text-white text-sm">
        &copy; 2023 Arrox. All Rights Reserved
      </div>
      </div>
    </div>
</template>

<script setup>

</script>