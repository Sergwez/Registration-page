<template>
  <div class="wrapper" @click.self="showLangSelect = false">
    <div class="form" @click.self="showLangSelect = false">
      <div class="form__title">Регистрация</div>
      <div class="form__subtitle">
        Уже есть аккаунт?
        <a class="form__subtitle-link" href="#">Войти</a>
      </div>
      <label class="form__name-label">Имя</label>
      <input
        :input="startNameValidation()"
        v-model="nameValue"
        class="form__name-input"
        placeholder="Введите Ваше имя"
      />
      <p v-if="nameValidation" class="form__name-error">
        Введено некорректное значение
      </p>

      <label class="form__email-label">E-mail</label>
      <input
        :input="startEmailValidation()"
        v-model="emailValue"
        class="form__email-input"
        placeholder="Введите ваш email"
      />
      <p v-if="emailValidation" class="form__email-error">
        Введено некорректное значение
      </p>

      <label class="form__phone-label">Номер телефона</label>
      <input
        :input="startPhoneValidation()"
        v-model="phoneValue"
        class="form__phone-input"
        placeholder="Введите номер телефона"
      />
      <p v-if="phoneValidation" class="form__phone-error">
        Введено некорректное значение
      </p>

      <label class="form__lang-label">Язык</label>
      <input
        class="form__input-lang"
        @focus="showLangSelect = true"
        type="text"
        :value="langValue"
        placeholder="Язык"
        readonly
      />
      <div class="form__select-group" v-show="showLangSelect">
        <label v-for="lang in langs" :key="lang" class="form__select-label">
          <input
            @click="showLangSelect = false"
            class="form__select-lang"
            v-model="langValue"
            :value="lang"
            type="radio"
          />
          {{ lang }}
        </label>
      </div>
      <label class="form__rules">
        <input
          class="form__rules-checkbox"
          v-model="checkedRules"
          type="checkbox"
        />
        <span class="form__rules-checkbox--img"></span>
        Принимаю
        <a class="form__rules-link" href="#">условия</a>
        использования
      </label>
      <input
        class="form__button"
        value="Зарегистрироваться"
        type="button"
        :disabled="!enableButton"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      langs: ["Русский", "Английский", "Испанский", "Китайский"],
      langValue: "",
      nameValue: "",
      emailValue: "",
      phoneValue: "",
      showLangSelect: false,
      nameValidation: false,
      emailValidation: false,
      phoneValidation: false,
      enableButton: false,
      checkedRules: false,
    };
  },
  methods: {
    startNameValidation: function () {
      if (this.nameValue) {
        let re = /^[a-zA-Zа-яёА-ЯЁ\s-]+$/;
        this.nameValidation = !re.test(this.nameValue);
        this.checkButton();
      } else {
        this.nameValidation = false;
      }
    },
    startEmailValidation: function () {
      if (this.emailValue) {
        let re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Zа-яёА-ЯЁ\-0-9]+\.)+[a-zA-Zа-яёА-ЯЁ]{2,}))$/;
        this.emailValidation = !re.test(this.emailValue);
        this.checkButton();
      } else {
        this.emailValidation = false;
      }
    },
    startPhoneValidation: function () {
      if (this.phoneValue) {
        let re = /^((\+|-|\(|\))*[0-9]{1}(\+|-|\(|\))*){11}$/;
        this.phoneValidation = !re.test(this.phoneValue);
        this.checkButton();
      } else {
        this.phoneValidation = false;
      }
    },
    checkButton: function () {
      if (
        !this.nameValidation &&
        !this.emailValidation &&
        !this.phoneValidation
      ) {
        if (
          this.nameValue &&
          this.emailValue &&
          this.phoneValue &&
          this.langValue &&
          this.checkedRules
        ) {
          this.enableButton = true;
        } else {
          this.enableButton = false;
        }
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@500&display=swap");
.wrapper {
  font-family: "IBM Plex Sans", sans-serif;
  font-size: 16px;
  color: #2c2738;
  background: #e5e5e5;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  min-height: 100vh;
  max-width: 100%;
}
.form {
  display: flex;
  flex-direction: column;
  max-width: 400px;
  width: 100%;
  min-width: 360px;
  border-radius: 24px;
  background: #ffffff;
  padding: 40px 30px 0 30px;
}
.form__title {
  font-size: 34px;
  font-weight: bold;
}
.form__subtitle {
  margin: 8px 0 -1px 0;
}
.form__subtitle-link {
  color: #0880ae;
  text-decoration: none;
}
.form__name-label,
.form__email-label,
.form__phone-label,
.form__lang-label {
  margin: 36px 0 7px 0;
  color: #756f86;
}
.form__name-label {
  margin: 60px 0 8px 0;
}
.form__name-input,
.form__email-input,
.form__phone-input,
.form__input-lang {
  font-family: "IBM Plex Sans", sans-serif;
  height: 50px;
  font-size: 16px;
  color: #2c2738;
  padding: 0px 0 0 14px;
  border: 1px solid #dbe2ea;
  border-radius: 6px;
  outline: none;
  max-width: 400px;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
}
.form__name-input:focus,
.form__email-input:focus,
.form__phone-input:focus,
.form__input-lang:focus {
  height: 48px;
  border: 2px solid #0880ae;
  padding: 0px 0 0 13px;
}
.form__name-input::placeholder,
.form__email-input::placeholder,
.form__phone-input::placeholder,
.form__input-lang::placeholder {
  color: #7c9cbf;
}
.form__name-error,
.form__email-error,
.form__phone-error {
  font-size: 14px;
  color: #ff7171;
  height: 15px;
  margin: 8px 0 -23px 0;
}
.form__select-group {
  display: flex;
  flex-direction: column;
}
.form__select-lang {
  display: none;
}
.form__input-lang {
  margin: 0 0 4px 0;
}
.form__select-group {
  display: flex;
  flex-direction: column;
  height: 0;
  overflow: visible;
  z-index: 1;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
    0px 20px 20px rgba(44, 39, 56, 0.04);
}
.form__input-lang {
  background-image: url("~@/assets/img/Chevron.svg");
  background-repeat: no-repeat;
  background-position: center right 11px;
}
.form__input-lang:focus {
  background-position: center right 10px;
}
.form__select-label {
  display: block;
  position: relative;
  background: #ffffff;
  padding: 16px 0 13px 15px;
  color: #756f86;
}
.form__select-label {
  border-left: 1px solid #dbe2ea;
  border-right: 1px solid #dbe2ea;
}
.form__select-label:first-of-type {
  border-radius: 6px 6px 0 0;
  border-top: 1px solid #dbe2ea;
}
.form__select-label:last-of-type {
  border-radius: 0 0 6px 6px;
  border-bottom: 1px solid #dbe2ea;
}
.form__select-label:hover {
  background: #ebf4f8;
}
.form__rules {
  margin: 27px 0 0 0;
  display: inline-flex;
  align-items: center;
  color: #756f86;
  white-space: pre;
}
.form__rules-checkbox {
  display: none;
}
.form__rules-checkbox:checked + .form__rules-checkbox--img {
  background-image: url("~@/assets/img/Checkbox.svg");
  background-position: center;
  border: 2px solid #0880ae;
  width: 24px;
  height: 24px;
}
.form__rules-checkbox--img {
  display: inline-block;
  border: 1px solid #dbe2ea;
  width: 26px;
  height: 26px;
  margin: 0 6px 0 0;
  border-radius: 4px;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
}
.form__rules-link {
  color: #0880ae;
  display: inline;
  text-decoration: none;
}
.form__button {
  font-family: "IBM Plex Sans", sans-serif;
  height: 56px;
  color: #ebf4f8;
  font-size: 16px;
  margin: 37px 0 40px 0;
  background: #0880ae;
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
    0px 4px 8px rgba(44, 39, 56, 0.08);
  border-radius: 6px;
  border: none;
  cursor: pointer;
  outline: none;
}
.form__button:hover {
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.08),
    0px 24px 48px rgba(44, 39, 56, 0.16);
}
.form__button:active {
  border: 2px solid rgba(44, 39, 56, 0.86);
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.0001),
    0px 4px 8px rgba(44, 39, 56, 0.08);
}
.form__button:disabled {
  background: #dbe2ea;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.08);
  color: #2c2738;
}
</style>
