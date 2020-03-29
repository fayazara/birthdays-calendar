<template>
  <div id="app" class="container mx-auto px-4 pt-20">
    <transition name="fade" mode="out-in">
      <div v-if="isLoading" :key="1">
        <Loader />
      </div>
      <div
        :key="2"
        v-else
        class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-2"
      >
        <Daycard
          v-for="(day, n) in daysOfweek"
          :key="n"
          :data="currentDayBdays(day)"
        />
      </div>
    </transition>
  </div>
</template>

<script>
import Daycard from './components/Daycard';
import Loader from './components/Loader';
import { API } from './api';

export default {
  data() {
    return {
      isLoading: false,
      daysOfweek: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
      birthdays: []
    };
  },
  components: {
    Daycard,
    Loader
  },
  methods: {
    segregateUsers: function(rawUserData) {
      this.daysOfweek.map(day => {
        var currentDay = rawUserData
          .map(user => {
            return {
              name: `${user.name.first} ${user.name.last}`,
              birthday: new Date(user.dob.date).toString().split(' ')[0],
              year: new Date(user.dob.date).toString().split(' ')[3]
            };
          })
          .filter(item => item.birthday === day);
        this.birthdays.push({
          day: day,
          birthday: currentDay
        });
      });
    },
    currentDayBdays(x) {
      return this.birthdays.filter(item => item.day == x)[0];
    }
  },
  mounted() {
    this.isLoading = true;
    API.get('api/?inc=name,dob&results=50&nat=us,dk,fr,gb').then(response => {
      this.segregateUsers(response.data.results);
      this.isLoading = false;
    });
  }
};
</script>

<style>
.bdays {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(75px, 1fr));
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
