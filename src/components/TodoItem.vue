<template>
  <div :class="`${color} w-full md:w-1/2 lg:w-1/3 xl:w-[28%] h-[20%] text-center mt-12 rounded-xl text-white m-4`">
    <h2 class="m-2 p-4 text-3xl font-bold">Title: {{ title }}</h2>
    <p class="m-4 p-4 text-xl">Description: {{ description }}</p>
    <div class="flex justify-center items-center">
      <button @click="$emit('delete')"
        class="bg-red-400 hover:bg-red-500 justify-center text-white mx-auto text-lg w-[30%] rounded-full m-4 p-4">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    description: String,
    color: String
  }
}
</script>

<!-- <style scoped></style> -->
