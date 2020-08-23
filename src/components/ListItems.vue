<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col" v-for="title in titleName" :key="title">{{ title }}</th>
      </tr>
    </thead>
    <tbody>
      <ListItem
        v-on:delete-user="removeUser"
        v-for="(user, index) of users"
        :user="user"
        :key="index + user"
        :index="index"
      />
    </tbody>
  </table>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
  name: 'ListItems',
  props: ['users', 'showModal', 'titleName'],
  components: {
    ListItem,
  },
  methods: {
    removeUser(id) {
      this.$emit('delete-user', id);
    },
  },
};
</script>

<style scope></style>
