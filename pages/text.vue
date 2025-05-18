<template>
  <div class="p-10">
    <h2 class="text-2xl mb-4">Hover over the text below:</h2>
    
    <DecryptedText 
      text="This text will decrypt on hover"
      class-name="text-green-500 font-bold"
      encrypted-class-name="text-red-500"
      sequential
    />
    
    <div class="mt-8">
      <DecryptedText 
        text="This will decrypt when scrolled into view"
        animate-on="view"
        class-name="text-blue-500 font-bold"
        encrypted-class-name="text-gray-500"
      />
    </div>
  </div>
</template>