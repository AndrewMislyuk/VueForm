<template>
  <form class="form" @submit.prevent="onSubmit">
    <div class="form__title">Welcome to OMG</div>
    <div class="form__item">
      <input
        type="text"
        class="form__input"
        v-model="name"
        :class="{
          validate:
            ($v.name.$dirty && !$v.name.required) ||
            ($v.name.$dirty && !$v.name.minLength),
          'form--label': name,
        }"
      />
      <label class="form__label">First Name</label>
    </div>
    <div class="form__item">
      <input
        type="text"
        class="form__input"
        v-model="surname"
        :class="{
          validate:
            ($v.surname.$dirty && !$v.surname.required) ||
            ($v.surname.$dirty && !$v.surname.minLength),
          'form--label': surname,
        }"
      />
      <label class="form__label">Last Name</label>
    </div>
    <div class="form__item long--input">
      <TheMask
        :mask="['+44 #### ######', '+44 #### ######']"
        type="text"
        class="form__input"
        v-model="phone"
        :class="{
          validate:
            ($v.phone.$dirty && !$v.phone.required) ||
            ($v.phone.$dirty && !$v.phone.minLength),
          'form--label': phone,
        }"
      />
      <label class="form__label">Phone</label>
    </div>
    <div class="form__item long--input">
      <input
        type="text"
        class="form__input"
        v-model="email"
        :class="{
          validate:
            ($v.email.$dirty && !$v.email.required) ||
            ($v.email.$dirty && !$v.email.email),
          'form--label': email,
        }"
      />
      <label class="form__label">Email</label>
    </div>
    <button
      type="submit"
      class="form__button"
      :disabled="
        !$v.name.required ||
          !$v.surname.required ||
          !$v.phone.required ||
          !$v.email.required
      "
    >
      Create Account
    </button>
  </form>
</template>

<script>
import { email, required, minLength } from "vuelidate/lib/validators";
import { TheMask } from "vue-the-mask";

export default {
  name: "form",
  data() {
    return {
      name: "",
      surname: "",
      phone: "",
      email: "",
    };
  },
  components: { TheMask },
  validations: {
    name: { required, minLength: minLength(3) },
    surname: { required, minLength: minLength(3) },
    phone: { required, minLength: minLength(10) },
    email: { email, required },
  },
  methods: {
    onSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      // Подготовка данных для бэкенда
      const formRegister = {
        name: this.name,
        surname: this.surname,
        phone: this.phone,
        email: this.email,
      };

      this.$router.push("/success");
    },
  },
};
</script>

<style lang="scss">
.form {
  position: relative;
  width: 570px;
  height: 341px;
  margin: 277px auto 0 auto;
}
.form__title {
  margin-bottom: 28px;
  text-align: center;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 26px;
  color: #333333;
}
.long--input input {
  width: 558px !important;
}
.form__item {
  display: inline-block;
  vertical-align: top;
  position: relative;
  margin-bottom: 16px;
  &:nth-child(2) {
    margin-right: 16px;
  }
}
.form__label {
  position: absolute;
  pointer-events: none;
  left: 28px;
  top: 20px;
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 19px;
  display: flex;
  align-items: center;
  letter-spacing: -0.01em;
  color: #7188a3;
  transition: 0.3s;
}
.form--label ~ .form__label,
.form--label:valid ~ .form--label {
  top: 11px;
  font-size: 10px;
  line-height: 14px;
}
.form__input:focus ~ .form__label,
.form__input:not(:focus):valid ~ .form__input {
  top: 11px;
  font-size: 10px;
  line-height: 14px;
}
.form__input {
  width: 270px;
  height: 58px;
  outline: none;
  border: none;
  background: #ffffff;
  box-shadow: 0px 1px 1px rgba(0, 66, 142, 0.25);
  border-radius: 10px;
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 19px;
  box-sizing: border-box;
  padding: 15px 28px 0;
  color: #000000;
}
.form__input:focus {
  box-sizing: border-box;
  padding: 15px 28px 0;
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 19px;
  color: #000000;
}
.form__input {
  &.validate {
    border: 1px solid #ff1a1a !important;
  }
}
.form__button {
  margin-top: 24px;
  position: absolute;
  right: 12px;
  bottom: 0;
  padding: 13px 33px;
  background: #01a3ff;
  border-radius: 60px;
  width: 204px;
  height: 51px;
  cursor: pointer;
  border: none;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
  line-height: 25px;
  text-align: center;
  letter-spacing: -0.02em;
  color: #fff;
  outline: none;

  &:disabled {
    cursor: auto;
    background: rgba(1, 163, 255, 0.25);
  }
}
</style>
