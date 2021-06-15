<template>
  <div class="w-full lg:w-1/2 m-auto p-2">
    <form action="">
      <div class="flex-col flex">
        <label for="name" class="font-medium">Nama Tugas</label>
        <input
          type="text"
          v-model="newNama"
          class="
            w-full
            px-4
            py-2
            my-2
            focus:outline-none
            border-2 border-indigo-700
            rounded-md
          "
          placeholder="Masukan Nama Tugas"
          required
        />
      </div>
      <div class="flex-col flex">
        <label for="deskripsi" class="font-medium">Deskripsi</label>
        <input
          type="text"
          v-model="newDeskripsi"
          class="
            w-full
            px-4
            py-2
            my-2
            focus:outline-none
            border-2 border-indigo-700
            rounded-md
          "
          placeholder="Wajib Mengisi Deskripsi !!"
          required
        />
      </div>
      <div class="flex flex-col">
        <label for="tanggal" class="font-medium">Masukkan Tanggal</label>
        <input
          type="date"
          v-model="newDate"
          class="
            border-2 border-indigo-700
            rounded-md
            px-4
            py-2
            focus:outline-none
          "
        />
      </div>

      <button
        @click.prevent="addTask"
        class="
          px-2
          py-2
          my-2
          bg-purple-700
          text-white
          rounded-sm
          focus:outline-none
        "
      >
        Masukkan Data
      </button>
    </form>
    <button
      class="
        px-2
        py-2
        border-2
        rounded-md
        border-indigo-700
        text-indigo-700
        focus:outline-none
      "
      @click="removeAll"
    >
      Hapus Semua
    </button>
  </div>
  <hr />
  <div class="w-full lg:w-1/2 m-auto my-3">
    <h1>Data Task</h1>
    <table class="w-full rounded-t-md overflow-hidden">
      <thead class="w-full items-start text-left">
        <tr class="bg-purple-700 text-white">
          <th class="p-2">Nama</th>
          <th>id</th>
          <th>Deskripsi</th>
          <th>Tanggal</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody class="w-full items-start text-left">
        <TableTask
          :key="task.id"
          v-for="task in tasks"
          :data="task"
          v-on:delete-todo="deleteTasks(task.id)"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import { ref, reactive, watch } from "vue";
import TableTask from "./TableTask.vue";

function loadTask() {
  const localTasks = localStorage.getItem("_touch_task");
  if (localTasks === null) {
    return [];
  } else {
    console.log("loda Task, loaded: " + localTasks);
    return JSON.parse(localTasks);
  }
}

function saveTasks(tasks) {
  localStorage.setItem("_touch_task", JSON.stringify(tasks));
}
export default {
  setup() {
    const newNama = ref("");
    const newDeskripsi = ref("");
    const newDate = ref("");

    const tasks = reactive(loadTask());

    function addTask() {
      tasks.push({
        id: Date.now(),
        nama: newNama.value,
        description: newDeskripsi.value,
        tanggal: newDate.value,
        done: false,
      });
      newNama.value = "";
      newDeskripsi.value = "";
      newDate.value = "";
    }

    function deleteTasks(id) {
      if (confirm("are you sure to delete task ?")) {
        console.log("delete taks widh id: " + id);
        for (let i = 0; i < tasks.length; i++) {
          if (tasks[i].id == id) {
            tasks.splice(i, 1);
            break;
          }
        }
      }
    }

    watch(tasks, (newTaks, prevTaks) => {
      saveTasks(newTaks);
    });
    function removeAll() {
      localStorage.removeItem("_touch_task");
    }
    return {
      tasks,
      newNama,
      newDeskripsi,
      newDate,
      addTask,
      deleteTasks,
      removeAll,
    };
  },
  components: {
    TableTask,
  },
};
</script>

<style></style>
