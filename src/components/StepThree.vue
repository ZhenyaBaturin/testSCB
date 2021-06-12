<template>
  <div class="container">
    <form class="form" action="" mrthod="GET">
      <h1>{{ msg }}</h1>
      <h3>Условие кредитования:</h3>
      <div class="form-sum">
        <div class="form-sum-block">
          <input
            class="form-sum_input input"
            type="number"
            min="50000"
            max="1000000"
            step="1000"
            placeholder="Сумма Кредита"
            name="credit_amount"
            required
          />
        </div>
        <fieldset class="form-sum_sel">
          <legend align="left">Срок кредита</legend>
          <select class="select input" name="credit_period" required>
            <option class="select" value="">Выберите из списка</option>
            <option value="1 year">на 1 год</option>
            <option value="2 years">на 2 года</option>
            <option value="3 years">на 3 года</option>
            <option value="4 years">на 4 года</option>
            <option value="5 years">на 5 лет</option>
          </select>
        </fieldset>
      </div>
      <div class="form-target">
        <fieldset class="form-target_sel">
          <legend align="left">Цель кредита</legend>
          <select class="select input" name="target_credit" required>
            <option value="" selected>Выберите из списка</option>
            <option value="healing">На лечение</option>
            <option value="construction">На строительство</option>
            <option value="study">На обучение</option>
          </select>
        </fieldset>
      </div>
      <h3>Паспортные данные:</h3>
      <div class="form-password">
        <input
          class="form-password_num input"
          type="number"
          min="1"
          placeholder="Серия и номер паспорта"
          name="passpord_number"
          required
        />
        <input
          class="form-password_data input"
          type="date"
          placeholder="Дата выдачи"
          name="date_issue_passport"
          required
        />
        <input
          class="form-password_code input"
          type="number"
          min="1"
          placeholder="Код подразделения"
          name="code_passport"
          required
        />
      </div>
      <div class="form-production">
        <input
          class="form-production_input input"
          type="text"
          placeholder="Орган выдачи"
          name="department_passport"
          required
        />
        <input
          class="form-production_place input"
          type="text"
          placeholder="Место рождения"
          name="date_of_birth"
          required
        />
      </div>
      <div class="form-registration">
        <input
          class="form-registration_adress input"
          type="text"
          placeholder="Адрес регистрации"
          name="adress_registration"
          required
        />
        <input
          class="form-registration_date input"
          type="date"
          placeholder="Дата регистрации"
          name="date_registration_data"
          required
        />
      </div>
      <div v-if="!registration" class="form-button">
        <button
          @click.prevent="registration = true"
          class="form-button_btn button"
        >
          Показать поля адреса
        </button>
      </div>
      <div v-if="registration" class="form-button">
        <button
          @click.prevent="registration = false"
          class="form-button_btn button"
        >
          Скрыть поля адреса
        </button>
      </div>
      <div v-if="registration" class="form-additionally">
        <input
          class="form-additionally_country input"
          type="text"
          placeholder="Страна"
          name="country"
        />
        <input
          class="form-additionally_region input"
          type="text"
          placeholder="Регион/Область"
          name="region"
        />
        <input
          class="form-additionally_town input"
          type="text"
          placeholder="Город"
          name="town"
        />
        <input
          class="form-additionally_street input"
          type="text"
          placeholder="Улица"
          name="street"
        />
      </div>
      <div class="form-checkbox">
        <input class="form-checkbox_input" type="checkbox" v-model="checkbox" />
        <label class="" for="">
          <span>Адрес проживания совпадает с адресом регистрации</span>
        </label>
      </div>
      <div class="form-living">
        <!-- <input
          class="form-living_input input"
          :class="getClass()"
          :disabled="checkbox"
          type="text"
          placeholder="Адрес проживания"
          name="adress_living"
        /> -->
        <Sugg />.
      </div>

      <div v-if="!living" class="form-button">
        <button
          @click.prevent="living = true"
          class="form-button_btn button"
          :disabled="checkbox"
        >
          Показать поля адреса
        </button>
      </div>
      <div v-if="living" class="form-button">
        <button @click.prevent="living = false" class="form-button_btn button">
          Скрыть поля адреса
        </button>
      </div>
      <div v-if="living" class="form-additionally">
        <input
          class="form-additionally_country input"
          type="text"
          placeholder="Страна"
          name="country"
          :class="getClass()"
          :disabled="checkbox"
        />
        <input
          class="form-additionally_region input"
          type="text"
          placeholder="Регион/Область"
          name="region"
          :class="getClass()"
          :disabled="checkbox"
        />
        <input
          class="form-additionally_town input"
          type="text"
          placeholder="Город"
          name="town"
          :class="getClass()"
          :disabled="checkbox"
        />
        <input
          class="form-additionally_street input"
          type="text"
          placeholder="Улица"
          name="street"
          :class="getClass()"
          :disabled="checkbox"
        />
      </div>

      <div class="form-method">
        <fieldset class="form-method_sel">
          <legend align="left">
            Условие проживания по фактическому адресу
          </legend>
          <select class="select input" name="accommodation_conditions" required>
            <option selected value="">Выберите из списка</option>
            <option value="owner">Вледение</option>
            <option value="rent">Аренда</option>
            <option value="with parents">Проживаю с родителями</option>
          </select>
        </fieldset>
      </div>
      <div class="form-location">
        <fieldset class="form-location_region">
          <legend align="left">Регион для оформления договора</legend>
          <select class="select input" name="registration_region" required>
            <option selected value="">Выберите из списка</option>
            <option value="Sverdlovsk">Свердловская область</option>
            <option value="Tatarstan">Татарстан</option>
            <option value="Rostov">Ростовская область</option>
            <option value="Kaluga">Калужская область</option>
          </select>
        </fieldset>
        <fieldset class="form-location_town">
          <legend align="left">Город для оформления договора</legend>
          <select class="select input" name="registration_town" required>
            <option selected value="">Выберите из списка</option>
            <option value="Ekaterinburg">Екатеринбург</option>
            <option value="Kazan">Казань</option>
            <option value="Rostov">Ростов</option>
            <option value="Kaluga">Калуга</option>
            <option value="Nizhny Tagil">Нижний Тагил</option>
            <option value="Pervouralsk">Первоуральск</option>
            <option value="Taganrog">Таганрок</option>
            <option value="Naberezhnye Chelny">Набережные Челны</option>
            <option value="Obninsk">Обнинск</option>
          </select>
        </fieldset>
        <fieldset class="form-location_office">
          <legend align="left">Офис для оформления договора</legend>
          <select class="select input" name="registration_office" required>
            <option selected value="">Выберите из списка</option>
            <option value="Uralmashevsky">
              Уралмашевский (г.Екатеринбург)
            </option>
            <option value="Golovnii">Головной (г.Екатеринбург)</option>
            <option value="Pionersky">Пионерский (г.Екатеринбург)</option>
            <option value="Vagonzavod">Вагонзавод (г.Нижний Тагил)</option>
            <option value="Kazansky">Казанский (г.Казань)</option>
            <option value="Donsky">Донской (г.Ростов)</option>
            <option value="Azovsky">Азовский (г.Таганрог)</option>
            <option value="Pervouralsky">
              Первоуральский (г.Первоуральск)
            </option>
            <option value="Kaluga">Калужский (г.Калуга)</option>
            <option value="Kamsky">Камский (г. Набережные Челны)</option>
          </select>
        </fieldset>
      </div>
      <div class="form-submit">
        <input class="form-submit-next btn" type="submit" value="Далее" />
        <input
          class="form-submit-reset btn"
          type="reset"
          @click="resetData"
          value="Отмена"
        />
      </div>
    </form>
  </div>
</template>

<script>
import Sugg from "./Sugg.vue";
// import VueDadata from './Dadata.vue'

export default {
  name: "StepThree",
  props: {
    msg: String,
  },
  data: function () {
    return {
      registration: false,
      living: false,
      checkbox: false,
      token: "92d9480112e42f8b923c3ad8ea5af68c46222760",
    };
  },

  methods: {
    getClass() {
      return {
        hidden: this.checkbox,
        "fa-checkbox-blank-outline": !this.checkbox,
      };
    },
    resetData() {
      (this.registration = false),
        (this.living = false),
        (this.checkbox = false);
    },
  },
  components: {
    Sugg,
    // VueDadata
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  font-family: "Source Sans Pro", sans-serif;
}
h3,
h1 {
  margin: 40px 0 0;
  text-align: left;
}
legend {
  font-size: 14px;
  align-items: left;
  font-family: "Times New Roman", Times, serif;
}
fieldset {
  border: 0.5px solid #ced6e0;
  border-radius: 5px;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 1170px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  padding: 50px 15px;
  box-shadow: inset 0 0 10px 5px rgba(0, 0, 0, 0.1);
}
.form {
  width: 95%;
}
.input {
  border-radius: 5px;
  box-shadow: none;
  border: 0.5px solid #ced6e0;
  transition: all 0.3s ease-in-out;
  font-size: 13px;
  padding: 15px 15px;
  background: none;
  color: #1a3b5d;
  font-family: "Source Sans Pro", sans-serif;
}
.select {
  border: 0;
  width: 100%;
  border: none;
  color: #8e8e8e;
  padding-top: 7px;
  outline: none;
}
.button {
  border: none;
  border-bottom: 1px dashed red;
  color: red;
  cursor: pointer;
  background-color: white;
  position: absolute;
  top: 0;
  right: 34%;
}
.btn {
  border-radius: 25px;
  padding: 15px 25px 15px 25px;
  cursor: pointer;
}
.btn:hover {
  opacity: 0.8;
  transform: scale(1.1);
}
.hidden {
  background-color: #e0dede;
}
.form-sum,
.form-submit,
.form-password,
.form-location {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  margin-bottom: 25px;
}
.form-sum {
  align-items: flex-end;
}
.form-sum_input {
  width: 100%;
}
.form-sum_sel,
.form-sum-block {
  width: 50%;
}
.form-sum-block {
  margin-right: 15px;
}
.form-target_sel {
  width: 100%;
}
.form-password_num,
.form-password_data,
.form-location_region,
.form-location_town {
  margin-right: 15px;
}

.form-password_code,
.form-password_num,
.form-password_data,
.form-location_region,
.form-location_town,
.form-location_office {
  width: 33%;
}
.form-production {
  display: flex;
  margin-bottom: 25px;
  flex-direction: column;
}
.form-production_input,
.form-method {
  margin-bottom: 25px;
}
.form-production_input,
.form-production_place,
.form-living_input {
  width: 66%;
}
.form-registration,
.form-living {
  display: flex;
  justify-content: space-between;
}
.form-registration_adress {
  width: 67%;
  margin-right: 15px;
}
.form-registration_date {
  width: 33%;
}
.form-registration-adress {
  margin-right: 15px;
}

.form-button {
  position: relative;
  padding-bottom: 15px;
  margin-bottom: 25px;
}

.form-checkbox {
  text-align: left;
  margin-bottom: 25px;
}
.form-checkbox_input {
  margin: 0 10px 0 20px;
}
.form-method {
  display: flex;
}
.form-method_sel {
  width: 50%;
}
.form-submit-reset {
  border: 0.5px solid rgb(238, 90, 90);
  color: rgb(238, 90, 90);
  background: none;
}
.form-submit-next {
  border: 0.5px solid rgb(238, 90, 90);
  background: rgb(238, 90, 90);
  color: white;
}
.form-additionally {
  display: flex;
  flex-direction: column;
}
.form-additionally_country,
.form-additionally_region,
.form-additionally_town,
.form-additionally_street {
  width: 66%;
  margin-bottom: 25px;
}
.form-additionally {
  transition: all 2s linear;
}
@media (max-width: 763px) {
  .input,
  .form-sum_sel,
  .form-method_sel,
  .form-location_region,
  .form-location_town,
  .form-location_office,
  .form-sum-block {
    width: 100%;
  }
  .form-sum-block {
    margin-right: 0;
  }
  .form-location_region,
  .form-location_town,
  input {
    margin-bottom: 15px;
  }
  .form-password,
  .form-sum,
  .form-registration,
  .form-location {
    flex-direction: column;
  }
  .button {
    right: 0;
  }
}
</style>
