<template>
  <div class="container">
    <form class="card" @submit.prevent="submitHandler">
      <h1>Анкета на Vue разработчика!</h1>
      <app-input
        placeholder="Введите имя"
        :error="errors.name"
        label="Как тебя зовут?"
        v-model:modelValue="name"
      ></app-input>

      <div class="form-control">
        <label for="age">Выбери возраст</label>
        <input type="number" id="age" v-model.number="age" max="65" />
      </div>

      <div class="form-control">
        <label for="city">Твой город</label>
        <select id="city" v-model="city">
          <option value="spb">Санкт-Петербург</option>
          <option value="msk">Москва</option>
          <option value="ekb">Екатеринбург</option>
          <option selected value="nsk">Новосибирск</option>
        </select>
      </div>

      <div class="form-checkbox">
        <span class="label">Готов к переезду в Токио?</span>
        <div class="checkbox">
          <label
            ><input type="radio" name="trip" v-model="relocate" value="yes" />
            Да</label
          >
        </div>

        <div class="checkbox">
          <label
            ><input type="radio" name="trip" v-model="relocate" value="no" />
            Нет</label
          >
        </div>
      </div>

      <div class="form-checkbox">
        <span class="label">Что знаешь во Vue?</span>
        <div class="checkbox">
          <label
            ><input
              type="checkbox"
              name="skills"
              v-model="vueSkills"
              value="vuex"
            />
            Vuex</label
          >
        </div>
        <div class="checkbox">
          <label
            ><input
              type="checkbox"
              name="skills"
              v-model="vueSkills"
              value="router"
            />
            Vue CLI</label
          >
        </div>
        <div class="checkbox">
          <label
            ><input
              type="checkbox"
              name="skills"
              v-model="vueSkills"
              value="CLI"
            />
            Vue Router</label
          >
        </div>
      </div>

      <div class="form-checkbox">
        <span class="label">Правила нашей компании</span>
        <div class="checkbox">
          <label
            ><input type="checkbox" v-model="agree" /> Согласен с
            правилами</label
          >
        </div>
      </div>

      <button type="submit" class="btn primary">Отправить</button>
    </form>
  </div>
</template>

<script>
import AppInput from "./components/AppInput";
export default {
  components: { AppInput },
  data() {
    return {
      name: "",
      age: 20,
      city: "msk",
      relocate: null,
      vueSkills: [],
      agree: false,
      errors: {
        name: null,
      },
    };
  },
  methods: {
    formIsValid() {
      let isValid = true;
      if (this.name.length === 0) {
        this.errors.name = "Имя не может быть пустым";
        isValid = false;
      } else {
        this.errors.name = null;
      }
      return isValid;
    },
    submitHandler() {
      if (this.formIsValid()) {
        console.group("formData");
        console.log("Name", this.name);
        console.log("Age", this.age);
        console.log("City", this.city);
        console.log("Relocate", this.relocate);
        console.log("Skills", this.vueSkills);
        console.log("Agree", this.agree);
        console.groupEnd();
      }
    },
  },
};
</script>

<style>
.form-control small {
  color: red;
}

.form-control.invalid input {
  border-color: red;
}
</style>
