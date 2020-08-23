<template>
  <div id="app">
    <transition name="model">
      <Modal v-on:add-user="addUser" v-if="showModal" :closeModal="closeModal" />
    </transition>
    <div class="card">
      <div class="card-header header">
        <h1 class="title">User Managment</h1>
        <ButtonAdd :showModalClick="showModalClick" />
      </div>
      <div class="card-body">
        <ListItems
          :titleName="titleName"
          :users="users"
          v-on:delete-user="removeUser"
          :swohModal="showModal"
        />
        <h5 class="card-title">Пагинация</h5>
        <p class="card-text"></p>
        <a href="http://localhost:8080" class="btn btn-primary">Домой</a>
      </div>
    </div>
  </div>
</template>

<script>
import ListItems from './components/ListItems.vue';
import Modal from './components/Modal.vue';
import ButtonAdd from './components/ButtonAdd.vue';

export default {
  name: 'App',
  data() {
    return {
      users: [
        {
          id: 1,
          name: 'Oleg 1',
          surname: 'Kolesnik',
          data: '20-08-1995',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
        {
          id: 2,
          name: 'Oleg 2',
          surname: 'Kolesnik',
          data: '2020-08-19',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
        {
          id: 3,
          name: 'Oleg 3',
          surname: 'Kolesnik',
          data: '2020-08-19',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
        {
          id: 4,
          name: 'Oleg 4',
          surname: 'Kolesnik',
          data: '2020-08-19',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
        {
          id: 5,
          name: 'Oleg 5',
          surname: 'Kolesnik',
          data: '2020-08-19',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
        {
          id: 6,
          name: 'Oleg 6',
          surname: 'Kolesnik',
          data: '2020-08-19',
          phone: '0632912138',
          email: 'justbloods28@gmail.com',
          create: 4,
        },
      ],
      titleName: [
        '#',
        'Имя',
        'Фамилия',
        'Дата рождения',
        'Номер телефона',
        'Почта',
        'Создание и обновление данных',
      ],
      showModal: false,
      isEditing: false,
      perPage: 10,
      currentPage: 1,
    };
  },
  components: {
    ListItems,
    Modal,
    ButtonAdd,
  },
  methods: {
    showModalClick() {
      this.showModal = !this.showModal;
    },
    closeModal() {
      this.showModal = false;
    },
    removeUser(id) {
      const user = this.users.findIndex((user) => user.id === id);

      this.users.splice(user, 1);
    },
    addUser(user) {
      this.users.push(user);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.header {
  display: flex;
  justify-content: space-between;
}
</style>
