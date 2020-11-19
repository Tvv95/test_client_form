<template>
  <form @submit.prevent="submitForm">
    <h2>Персональные данные</h2>
    <div class="formPart">
      <label for="surname"
        >Фамилия*:
        <p
          v-if="
            $v.personalInfo.surname.$dirty && !$v.personalInfo.surname.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p></label
      >
      <input
        type="text"
        id="surname"
        v-model.trim="personalInfo.surname"
        :class="$v.personalInfo.surname.$error ? 'invalid' : ''"
      />
      <label for="name"
        >Имя*:
        <p
          v-if="$v.personalInfo.name.$dirty && !$v.personalInfo.name.required"
          class="invalidMsg"
        >
          Обязательное поле !
        </p></label
      >
      <input
        type="text"
        id="name"
        v-model.trim="personalInfo.name"
        :class="$v.personalInfo.name.$error ? 'invalid' : ''"
      />
      <label for="middleName">Отчество:</label>
      <input
        type="text"
        id="middleName"
        v-model.trim="personalInfo.middleName"
      />
      <label for="birthday"
        >Дата рождения*:
        <p
          v-if="
            $v.personalInfo.birthday.$dirty &&
            !$v.personalInfo.birthday.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
      </label>
      <input
        type="date"
        id="birthday"
        v-model="personalInfo.birthday"
        :class="$v.personalInfo.birthday.$error ? 'invalid' : ''"
      />
      <label for="phoneNumber"
        >Номер телефона*:
        <p
          v-if="
            $v.personalInfo.phoneNumber.$dirty &&
            !$v.personalInfo.phoneNumber.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
        <p
          v-else-if="
            $v.personalInfo.phoneNumber.$dirty &&
            !$v.personalInfo.phoneNumber.phoneValidate
          "
          class="invalidMsg"
        >
          Недопустимый формат номера !
        </p>
      </label>
      <input
        @click="handlerPhone"
        type="tel"
        id="phoneNumber"
        placeholder="+7 XXX XXX XX XX"
        v-model.trim="personalInfo.phoneNumber"
        :class="$v.personalInfo.phoneNumber.$error ? 'invalid' : ''"
      />
      <label for="gender">Пол:</label>
      <select id="gender" v-model="personalInfo.gender">
        <option>Мужской</option>
        <option>Женский</option>
      </select>
      <label for="clientGroup"
        >Группа клиентов*:
        <p
          v-if="
            $v.personalInfo.clientGroup.$dirty &&
            !$v.personalInfo.clientGroup.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
      </label>
      <select
        multiple
        id="clientGroup"
        v-model="personalInfo.clientGroup"
        :class="$v.personalInfo.phoneNumber.$error ? 'invalid' : ''"
      >
        <option>VIP</option>
        <option>Проблемные</option>
        <option>ОМС</option>
      </select>
      <label for="doctorName">Лечащий врач:</label>
      <select id="doctorName" v-model="personalInfo.doctorName">
        <option>Иванов</option>
        <option>Захаров</option>
        <option>Чернышева</option>
      </select>
      <label for="smsNotSend">Не отправлять СМС:</label>
      <input type="checkbox" id="smsSend" v-model="personalInfo.smsSend" />
    </div>
    <h2>Адрес</h2>
    <div class="formPart">
      <label for="postCode"
        >Индекс:
        <p
          v-if="
            $v.adress.postCode.$dirty &&
            (!$v.adress.postCode.minLength || !$v.adress.postCode.maxLength)
          "
          class="invalidMsg"
        >
          Недопустимый формат индекса !
        </p>
      </label>
      <input
        type="number"
        id="postCode"
        v-model.trim="adress.postCode"
        placeholder="XXXXXX"
        :class="$v.adress.postCode.$error ? 'invalid' : ''"
      />
      <label for="country">Страна:</label>
      <input type="text" id="country" v-model="adress.country" />
      <label for="region">Область:</label>
      <input type="text" id="region" v-model="adress.region" />
      <label for="city"
        >Город*:
        <p
          v-if="$v.adress.city.$dirty && !$v.adress.city.required"
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
      </label>
      <input
        type="text"
        id="city"
        v-model="adress.city"
        :class="$v.adress.city.$error ? 'invalid' : ''"
      />
      <label for="street">Улица:</label>
      <input type="text" id="street" v-model="adress.street" />
      <label for="house">Дом:</label>
      <input type="text" id="house" v-model="adress.house" />
    </div>
    <h2>Паспорт</h2>
    <div class="formPart">
      <label for="documentType"
        >Тип документа*:
        <p
          v-if="
            $v.passport.documentType.$dirty &&
            !$v.passport.documentType.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
      </label>
      <select
        id="documentType"
        v-model="passport.documentType"
        :class="$v.passport.documentType.$error ? 'invalid' : ''"
      >
        <option>Паспорт</option>
        <option>Свидетельство о рождении</option>
        <option>Вод. удостоверение</option>
      </select>
      <label for="docSeries">Серия:</label>
      <input type="text" id="docSeries" v-model.trim="passport.docSeries" />
      <label for="docNumber">Номер:</label>
      <input type="number" id="docNumber" v-model.trim="passport.docNumber" />
      <label for="docIssue">Кем выдан:</label>
      <input type="text" id="docIssue" v-model="passport.docIssue" />
      <label for="docDateIssue"
        >Дата выдачи*:
        <p
          v-if="
            $v.passport.docDateIssue.$dirty &&
            !$v.passport.docDateIssue.required
          "
          class="invalidMsg"
        >
          Обязательное поле !
        </p>
      </label>
      <input
        type="date"
        id="docDateIssue"
        v-model="passport.docDateIssue"
        :class="$v.passport.documentType.$error ? 'invalid' : ''"
      />
    </div>
    <p class="submitMessage" v-if="formSended === true">
      Клиент успешно создан
    </p>
    <button type="submit">Отправить</button>
  </form>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, minLength, maxLength } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],
  data() {
    return {
      formSended: false,
      personalInfo: {
        surname: "",
        name: "",
        middleName: "",
        birthday: "",
        phoneNumber: "",
        gender: "",
        clientGroup: [],
        doctorName: "",
        smsNotSend: false,
      },
      adress: {
        postCode: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      passport: {
        documentType: "",
        docSeries: "",
        docNumber: "",
        docIssue: "",
        docDateIssue: "",
      },
    };
  },
  validations: {
    personalInfo: {
      surname: {
        required,
      },
      name: {
        required,
      },
      birthday: {
        required,
      },
      phoneNumber: {
        required,
        phoneValidate(value) {
          return /\+7\d{10}$/.test(value);
        },
      },
      clientGroup: {
        required,
      },
    },
    adress: {
      postCode: {
        minLength: minLength(6),
        maxLength: maxLength(6),
      },
      city: {
        required,
      },
    },
    passport: {
      documentType: {
        required,
      },
      docDateIssue: {
        required,
      },
    },
  },
  methods: {
    handlerPhone() {
      if (this.personalInfo.phoneNumber === "") {
        this.personalInfo.phoneNumber = "+7";
      }
    },
    submitForm() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      Object.assign(this.$data, this.$options.data.call(this));
      this.formSended = true;
    },
  },
};
</script>

<style scoped lang="scss">
form {
  width: 80%;
  max-width: 650px;
  margin: 1% auto;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
  padding: 20px;
  border-radius: 10px;
  background-color: #ffffff;
  .formPart {
    display: flex;
    flex-direction: column;
    background-color: #f8f8f8;
    padding: 20px;
    border-radius: 10px;
  }
  h2 {
    margin: 10px 0;
    margin-left: 5px;
    color: #2a88ad;
  }
  label {
    margin-bottom: 3px;
  }
  input,
  select {
    margin-bottom: 10px;
    border: 2px solid #ffffff;
    border-radius: 5px;
    box-shadow: inset 0px 1px 1px rgba(0, 0, 0, 0.33);
  }
  input:not([type="checkbox"]),
  select:not([multiple]) {
    height: 20px;
  }
  input[type="date"] {
    cursor: text;
  }
  select {
    cursor: pointer;
  }
  button {
    background: #2a88ad;
    max-width: 110px;
    padding: 8px 20px 8px 20px;
    border-radius: 5px;
    color: #ffffff;
    display: block;
    margin-left: auto;
    margin-right: 2%;
    margin-top: 20px;
    cursor: pointer;
    &:hover {
      background: #2a6881;
      box-shadow: inset 0px 2px 2px 0px rgba(255, 255, 255, 0.3);
    }
  }
  .submitMessage {
    text-align: right;
    color: green;
  }
  .invalidMsg {
    margin: 0;
    float: right;
    color: red;
  }
  .invalid {
    border-color: red !important;
  }
}
</style>