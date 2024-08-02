<template>
  <div class="contact-form">
    <form @submit.prevent="validateForm">
      <div class="form-columns">
        <div class="form-section left-section">
          <h2>ПРЕДСТАВТЕСЯ, БУДЬ ЛАСКА</h2>
          <div class="form-group">
            <label>* Прізвище</label>
            <input v-model="form.surname" type="text" :class="{'is-invalid': errors.surname}" />
          </div>
          <div class="form-group">
            <label>* Ім'я </label>
            <input v-model="form.name" type="text" :class="{'is-invalid': errors.name}" />
          </div>
          <div class="form-group">
            <label>Організація та посада</label>
            <input v-model="form.organization" type="text" />
          </div>
          <div class="form-group">
            <div class="radio-group">
              <label>
                <input type="radio" v-model="form.userType" value="СПОЖИВАЧ" />
                <span class="radio-btn"></span> СПОЖИВАЧ
              </label>
              <label>
                <input type="radio" v-model="form.userType" value="МЕДИЧНИЙ ПРАЦІВНИК" />
                <span class="radio-btn"></span> МЕДИЧНИЙ ПРАЦІВНИК
              </label>
              <label>
                <input type="radio" v-model="form.userType" value="ЖУРНАЛІСТ" />
                <span class="radio-btn"></span> ЖУРНАЛІСТ
              </label>
            </div>
          </div>
          <div class="form-group">
            <label>Тема повідомлення</label>
            <input v-model="form.subject" type="text" />
          </div>
          <div class="form-group">
            <label>* Повідомлення</label>
            <textarea v-model="form.message" :class="{'is-invalid': errors.message}"></textarea>
          </div>
        </div>
        <div class="form-section right-section">
          <h2>Контактна інформація</h2>
          <div class="form-group">
            <label>* Email</label>
            <input v-model="form.email" type="email" :class="{'is-invalid': errors.email}" />
          </div>
          <div class="form-group">
            <label>Країна</label>
            <input v-model="form.country" type="text" />
          </div>
          <div class="form-group">
            <label>Місто</label>
            <input v-model="form.city" type="text" />
          </div>
          <div class="form-group">
            <label>Індекс</label>
            <input v-model="form.zip" type="text" />
          </div>
          <div class="form-group">
            <label>Адреса</label>
            <input v-model="form.address" type="text" />
          </div>
          <div class="form-group">
            <label>* Телефон</label>
            <input v-model="form.phone" type="text" :class="{'is-invalid': errors.phone}" @input="formatPhone" />
          </div>
          <div class="form-actions">
            <button type="submit">ВІДПРАВИТИ</button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        surname: '',
        name: '',
        organization: '',
        userType: '',
        subject: '',
        message: '',
        email: '',
        country: '',
        city: '',
        zip: '',
        address: '',
        phone: ''
      },
      errors: {
        surname: false,
        name: false,
        message: false,
        email: false,
        phone: false
      }
    };
  },
  methods: {
    validateForm() {
      this.clearErrors();

      const kirillicaRegex = /^[А-Яа-яЁёЇїІіЄєҐґ\s-]+$/;
      const kirillicaAndDigitsRegex = /^[А-Яа-яЁёЇїІіЄєҐґ0-9\s,./-]+$/;
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      const phoneDigitsRegex = /^\d{10}$/;

      let valid = true;

      // Валидация обязательных полей
      if (!kirillicaRegex.test(this.form.surname)) {
        this.errors.surname = true;
        valid = false;
      }
      if (!kirillicaRegex.test(this.form.name)) {
        this.errors.name = true;
        valid = false;
      }
      if (!kirillicaAndDigitsRegex.test(this.form.message)) {
        this.errors.message = true;
        valid = false;
      }
      if (!emailRegex.test(this.form.email)) {
        this.errors.email = true;
        valid = false;
      }
      // Проверка номера телефона: если поле заполнено, проверяем только цифры
      const phoneDigits = this.form.phone.replace(/\D/g, '');
      if (this.form.phone.trim() === '' || !phoneDigitsRegex.test(phoneDigits)) {
        this.errors.phone = true;
        valid = false;
      }

      if (valid) {
        alert('Відправлено');
      } else {
        alert('Будь ласка, заповніть всі обов\'язкові поля правильно.');
      }
    },
    clearErrors() {
      for (const key in this.errors) {
        this.errors[key] = false;
      }
    },
    formatPhone(event) {
      let value = event.target.value.replace(/\D/g, '');
      if (value.length > 10) value = value.slice(0, 10);
      this.form.phone = value;
      let formattedPhone = '';
      if (value.length > 0) {
        formattedPhone = `(${value.slice(0, 3)}`;
      }
      if (value.length > 3) {
        formattedPhone += `) ${value.slice(3, 6)}`;
      }
      if (value.length > 6) {
        formattedPhone += `-${value.slice(6, 8)}`;
      }
      if (value.length > 8) {
        formattedPhone += `-${value.slice(8)}`;
      }
      event.target.value = formattedPhone;
    }
  }
};

</script>

<style scoped>
.contact-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
}

.form-columns {
  text-transform: uppercase;
  display: flex;
  justify-content: space-between;
}

.form-section {
  width: 48%;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

.form-group .is-invalid {
  border-color: red;
}

.radio-group {
  display: flex;
  flex-direction: column;
}

.radio-group label {
  display: flex;
  align-items: center;
}

.radio-group input[type="radio"] {
  display: none;
}

.radio-group .radio-btn {
  width: 20px;
  height: 20px;
  border: 2px solid #000;
  border-radius: 50%;
  margin-right: 10px;
  position: relative;
}

.radio-group input[type="radio"]:checked + .radio-btn::after {
  content: '';
  width: 12px;
  height: 12px;
  background: red;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.form-actions {
  display: flex;
  justify-content: flex-start;
  margin-top: 20px;
}

button {
  background-color: #464646;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 5px;
  width: 246px;
  height: 31px;
}

button:hover {
  background-color: #555;
}

@media (max-width: 768px) {
  .form-columns {
    flex-direction: column;
  }

  .form-section {
    width: 100%;
    margin-bottom: 20px;
  }
}
@media (max-width: 768px) {
  .form-columns {
    flex-direction: column;
  }

  .form-section {
    width: 100%;
    margin-bottom: 20px;
  }
}

@media (max-width: 320px) {
  .contact-form {
    padding: 10px; /* Уменьшаем отступы для меньших экранов */
  }

  .form-group {
    margin-bottom: 10px; /* Уменьшаем отступ между группами полей */
  }

  .radio-group .radio-btn {
    width: 16px;
    height: 16px;
  }

  .form-actions {
    justify-content: center; /* Выравниваем кнопку по центру на очень маленьких экранах */
  }

  button {
    width: 100%; /* Кнопка занимает всю ширину доступного пространства */
    height: auto; /* Позволяет кнопке адаптироваться по высоте */
    padding: 10px; /* Увеличиваем внутренние отступы кнопки для лучшего взаимодействия */
  }
}
</style>
