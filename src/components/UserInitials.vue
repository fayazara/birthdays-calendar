<template>
  <div class="h-16 flex justify-center items-center" :class="`bg-${color}-700`">
    <span class="text-white">{{ getInitials(bday.name) }}</span>
  </div>
</template>

<script>
export default {
  props: ['bday'],
  data() {
    return {
      colors: [
        'gray',
        'red',
        'green',
        'orange',
        'yellow',
        'teal',
        'indigo',
        'purple',
        'pink'
      ]
    };
  },
  computed: {
    color() {
      return this.colors[Math.floor(Math.random() * this.colors.length)];
    }
  },
  methods: {
    getInitials: function(name) {
      return name
        .split(' ')
        .map(n => n[0])
        .join('');
    }
  }
};
</script>

<style></style>
