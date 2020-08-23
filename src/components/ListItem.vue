<template>
  <tr class="input">
    <th class="th-list" scope="row">{{ index }}</th>
    <td class="th-list" v-show="isEditing">
      <input
        maxlength="60"
        minlength="1"
        type="text"
        class="input input-name"
        v-model="user.name"
      />
    </td>
    <td class="th-list" v-show="!isEditing">{{ user.name }}</td>
    <td class="th-list" v-show="isEditing">
      <input
        maxlength="60"
        minlength="1"
        type="text"
        class="input input-surname"
        v-model="user.surname"
      />
    </td>
    <td class="th-list" v-show="!isEditing">{{ user.surname }}</td>
    <td class="th-list" v-show="isEditing">
      <input type="date" class="input input-data" v-model="user.data" />
    </td>
    <td class="th-list" v-show="!isEditing">{{ user.data }}</td>
    <td class="th-list" v-show="isEditing">
      <input type="number" class="input input-phone" v-model="user.phone" />
    </td>
    <td class="th-list" v-show="!isEditing">{{ user.phone }}</td>
    <td class="th-list" v-show="isEditing">
      <input type="email" class="input input-email" v-model="user.email" />
    </td>
    <td class="th-list" v-show="!isEditing">{{ user.email }}</td>
    <td class="th-list" v-show="isEditing"></td>
    <td class="th-list" v-show="!isEditing">{{ new Date().toUTCString() }}</td>
    <td>
      <button @click="$emit('delete-user', user.id)" type="button" class="btn btn-danger delete">
        Delete</button
      ><button v-show="!isEditing" @click="showForm" type="button" class="btn btn-info">
        Update
      </button>
      <button v-show="isEditing" @click="hideForm" type="submit" class="btn btn-info">
        Save
      </button>
    </td>
  </tr>
</template>

<script>
export default {
  name: 'ListItem',
  data() {
    return {
      isEditing: false,
    };
  },
  props: {
    user: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
  },
};
</script>

<style scoped>
.th-list {
  padding: 0;
  margin: 0;
}
.input {
  padding: 0;
  margin: 4px 0 0 0;
}

.delete {
  margin-right: 4%;
}
</style>
