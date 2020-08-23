<template>
  <div class="modal" tabindex="2" role="dialog">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Добавить нового пользователя</h5>
          <button
            type="button"
            @click="closeModal"
            class="close"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <p class='error-logo' v-if="errors.length">
              <b>Пожалуйста исправьте указанные ошибки:</b>
              <ul>
                <li v-for="(error, index) in errors" :key="error + index" >{{ error }}</li>
              </ul>
            </p>
          <form @submit="checkForm">
            <div class="form-group">
              <label for="recipient-name" class="col-form-label">Имя:</label>
              <input
                maxlength="60"
                minlength="1"
                type="text"
                class="form-control"
                id="recipient-name"
                v-model="name"
              />
            </div>
            <div class="form-group">
              <label for="recipient-name" class="col-form-label">Фамилия:</label>
              <input
                maxlength="60"
                minlength="1"
                type="text"
                class="form-control"
                id="recipient-name"
                v-model="surname"
              />
            </div>
            <div class="form-group">
              <label for="recipient-name" class="col-form-label">Дата рождения:</label>
              <input type="date" class="form-control" id="recipient-name" v-model="dataYear" />
            </div>
            <div class="form-group">
              <label for="recipient-name" class="col-form-label">Номер телефона:</label>
              <input
                maxlength="8"
                type="number"
                class="form-control"
                id="recipient-name"
                v-model="phone"
              />
            </div>
            <div class="form-group">
              <label for="recipient-name" class="col-form-label">Почта:</label>
              <input type="text" class="form-control" id="recipient-name" v-model="email" />
            </div>
            <div class="modal-footer">
              <button
                @click="closeModal"
                type="button"
                class="btn btn-secondary"
                data-dismiss="modal"
              >
                Close
              </button>
              <input
                type="submit"
                @click="addItem"
                value="Save changes"
                class="btn btn-primary" />
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: ['users', 'closeModal'],
  data() {
    return {
      errors: [],
      name: null,
      surname: null,
      email: null,
      dataYear: null,
      phone: null,
    };
  },
  methods: {
    checkForm: function(e) {
      this.errors = [];

      if (!this.name) {
        this.errors.push('Укажите имя.');
      }
      if (!this.surname) {
        this.errors.push('Укажите фамилию.');
      }
      if (!this.dataYear) {
        this.errors.push('Укажите дату рождения.');
      }
      if (!this.phone) {
        this.errors.push('Укажите номер телефона.');
      }
      if (!this.email) {
        this.errors.push('Укажите электронную почту.');
      } else if (!this.validEmail(this.email)) {
        this.errors.push('Укажите корректный адрес электронной почты.');
      }

      if (!this.errors.length) {
        return true;
      }

      e.preventDefault();
    },
    validEmail: function(email) {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },

    addItem(e) {
      const newUser = {
        id: Math.random(),
        phone: this.phone,
        name: this.name,
        surname: this.surname,
        email: this.email,
        data: this.dataYear,
        create: new Date().toUTCString(),
      }
        this.$emit('add-user', newUser)
        this.closeModal()
        e.preventDefault()
    },
  },
};
</script>

<style>
.error-logo ul {
  display: flex;
  padding: 0;
  margin: 0;
  font-size: 12px;
}
.error-logo ul li {
  margin-right: 4%;
}

.error-logo b {
  font-size: 12px;
}

div .modal {
  display: block;
  width: 100%;
  height: 100%;
  outline: 0;
  background: rgba(225, 225, 225, 0.9);
  padding-bottom: 10px;
}
</style>
