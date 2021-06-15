<template>
 <tr>
        <td>{{ data.nama }}</td>
  <td>{{ data.id }}</td>
  <td>{{ data.description }}</td>
  <td>{{ data.tanggal }}</td>
  <td v-if="data.done">
    <button @click="$emit('delete-todo')">Delete</button>
  </td>
  <td v-else>
    <!-- <input type="checkbox" v-model="data.done" :checked="data.done" /> -->
    <button @click="data.done = !data.done">Selesai</button>
  </td>
 </tr>
</template>

<script>
export default {
  props: {
    data: Object,
  },
};
</script>

<style>
</style>