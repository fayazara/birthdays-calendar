<template>
  <div class="bg-gray-200 rounded shadow border">
    <div class="p-4 bg-indigo-500 rounded-t">
      <p class="text-white">{{ data.day }}</p>
    </div>
    <div class="bdays">
      <UserInitials v-for="(bday, i) in data.birthday"
        :key="i" :bday="bday"/>
    </div>
  </div>
</template>

<script>
import UserInitials from '../components/UserInitials'
export default {
  props: ['data'],
  components: {
    UserInitials
  }
};
</script>
