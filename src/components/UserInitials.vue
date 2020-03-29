<template>
  <div
    class="increament-z h-16 flex justify-center items-center transform hover:scale-105 transition ease-out duration-500"
    :class="`bg-${color}-600`"
  >
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

<style>
.increament-z:hover {
  z-index: 99 !important;
}
</style>
