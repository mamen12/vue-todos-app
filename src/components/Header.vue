<template>
  <div class="w-full h-1/6 flex justify-center text-center bg-purple-700 text-white py-4 font-bold lg:text-4xl lg:py-10 lg:w-1/2 m-auto rounded-b-md"> {{title}}</div>
</template>

<script>
export default {
  name: "Header",
  props: ['title'],
};
</script>

<style>
</style>