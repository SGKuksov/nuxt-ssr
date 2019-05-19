<template>
  <div class="user">
    <h3>{{ user.name }}</h3>
    <h4>@{{ user.username }}</h4>
    <p>Email : {{ user.email }}</p>
    <p><nuxt-link to="/">List of users</nuxt-link></p>
  </div>
</template>

<script>
// import axios from 'axios';
import { mapState, mapActions, mapGetters } from 'vuex';

export default {
  computed: {
    ...mapGetters(['userById', 'isFetched']),
    user() {
      return this.userById(this.$route.params.id);
    },
  },
  methods: {
    ...mapActions(['fetchUsers'])
  },
  async fetch({ store }) {
    if (!this.isFetched) {
      return store.dispatch('fetchUsers');
    }
  },
}
</script>

<style scoped>
  .user {
    text-align: center;
    margin-top: 100px;
    font-family: sans-serif;
  }
</style>
