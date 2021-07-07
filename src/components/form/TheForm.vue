<template>
  <base-dialog :show="isVisible" title="Example">
    <template #default>
      <p>Новый клиент успешно создан</p>
    </template>
  </base-dialog>
  <form @submit.prevent="checkValidation">
    <div class="atr">
      <h3>Общие данные</h3>
      <span class="line"></span>
      <p><sup>*</sup> отмечены обязательные поля для заполнения</p>
      <label for="lastName">Фамилия<sup>*</sup></label>
      <input id="lastName" type="text" v-model.trim="lastName">
      <span class="error--valid">{{ lastNameError }}</span>
      <label for="firstName">Имя<sup>*</sup></label>
      <input id="firstName" type="text" v-model.trim="firstName">
      <span class="error--valid">{{ firstNameError }}</span>
      <label for="fatherhood">Отчество</label>
      <input id="fatherhood" type="text">
      <label for="birthday">Дата рождения<sup>*</sup></label>
      <input id="birthday" type="date" v-model.trim="birthday">
      <span class="error--valid value">{{ birthdayError }}</span>
      <label for="phone">Номер тел.<sup>*</sup></label>
      <input type="tel"  name="phone_number" id="phone" placeholder="+7 (900) 123-45-67" v-model.trim="numberPhone">
      <span class="error--valid value">{{ numberPhoneError }}</span>
      <div class="check">
        <input id="male" name="gender" type="radio" value="male">
        <label for="male">Male</label>
        <input id="female" name="gender" type="radio" value="female">
        <label for="female">Female</label>
      </div>
      <label for="kind">Группа клиентов<sup>*</sup></label>
      <select id="kind" class="select-css" multiple name="kind of clients" size="3">
        <option>VIP</option>
        <option>Проблемные</option>
        <option>ОМС</option>
      </select>
      <label for="doctor">Лечащий врач</label>
      <select id="doctor" class="select-css" name="doctor">
        <option value="Iv">Иванов</option>
        <option value="Za">Захаров</option>
        <option value="Che">Чернышева</option>
      </select>
      <div class="check">
        <label for="sms">Не отправлять СМС.</label>
        <input id="sms" name="sms" type="checkbox">
      </div>
      <h3>Адрес</h3>
      <span class="line"></span>
      <label for="index">Индекс</label>
      <input id="index" name="index" type="number">
      <label for="country">Страна</label>
      <input id="country" name="country" type="text">
      <label for="region">Регион</label>
      <input id="region" name="region" type="text">
      <label for="town">Город<sup>*</sup></label>
      <input id="town" name="town" type="text">
      <label for="street">Улица</label>
      <input id="street" name="street" type="text">
      <label for="house">Дом</label>
      <input id="house" name="house" type="text">
      <h3>Паспорт</h3>
      <span class="line"></span>
      <label for="doc">Тип документа<sup>*</sup></label>
      <select id="doc" class="select-css" name="kindDocument">
        <option value="passport">Паспорт</option>
        <option value="certificate">Свидетельство о рождении</option>
        <option value="driversLicense">Водительское удостоверение</option>
      </select>
      <label for="series">Серия</label>
      <input id="series" name="series" type="text">
      <label for="number">Серия</label>
      <input id="number" name="number" type="text">
      <label for="by">Кем выдан</label>
      <input id="by" name="by" type="text">
      <label for="date">Дата выдачи<sup>*</sup></label>
      <input id="date" name="date" type="date">
      <button class="button" >Submit</button>
    </div>
  </form>
</template>

<script>
// import { ref } from 'vue'
import { useForm, useField } from 'vee-validate'

export default {
  setup () {
    let isValidate = true
    // functions ..
    function checkRequired (value) {
      isValidate = true
      if (value === '') {
        isValidate = false
        return 'это поле обязательное для заполнения'
      }
      return true
    }
    // Define a validation schema
    const mySchema = {
      lastName (value) {
        return checkRequired(value)
      },
      firstName (value) {
        return checkRequired(value)
      },
      birthday (value) {
        return checkRequired(value)
      },
      numberPhone (value) {
        if (value[1] !== '7') return 'номер должен начинаться с +7'
        if (value.length > 16) return 'номер должен быть не больше 11 чисел'
        return true
      }
    }

    // Create a form context with the validation schema
    useForm({
      validationSchema: mySchema
    })

    // No need to define rules for fields
    const {
      value: lastName,
      errorMessage: lastNameError
    } = useField('lastName')
    const {
      value: firstName,
      errorMessage: firstNameError
    } = useField('firstName')
    const {
      value: birthday,
      errorMessage: birthdayError
    } = useField('birthday')
    const {
      value: numberPhone,
      errorMessage: numberPhoneError
    } = useField('numberPhone')
    function checkValidation () {
      console.log(isValidate)
    }
    return {
      lastName,
      lastNameError,
      firstName,
      firstNameError,
      birthday,
      birthdayError,
      numberPhone,
      numberPhoneError,
      checkValidation
    }
  }
}
</script>

<style lang="scss" scoped>
$main-color: #42b983;
$hover-color: #888;

form .atr {
  margin: 0 auto;
  padding: 1rem 0.5rem;
  border: 2px solid $main-color;
  border-radius: 10px;
  display: grid;
  gap: 0.4rem 0;
  justify-content: center;
  align-items: center;
  max-width: 1000px;
  @media (min-width: 40rem) {
    grid-template-columns: 20% auto;
    font-size: 1.3rem;
  }
}

label {
  text-align: left;
  @media (min-width: 40rem) {
  }
}

input:not([name="gender"]) {
  height: 2rem;
  border-radius: 10px;
  border: 0.3px solid $main-color;
  background: rgba(255,255,255,0.04)

}

input:hover {
  border-color: $hover-color;
}

.check {
  border: 0.5px solid $main-color;
  border-radius: 10px;
  height: 2rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  @media (min-width: 40rem) {
    grid-column: span 2;
  }
}

p {
  font-size: 0.8rem;
  color: $main-color;
  @media (min-width: 40rem) {
    grid-column: span 2;
  }
}

.line {
  display: block;
  border: 2px solid $main-color;
}

.button {
  @media (min-width: 40rem) {
    grid-column: span 2;
    width: 10rem;
    justify-self: center;
  }
}

.select-css {
  display: block;
  font-size: 16px;
  font-weight: 700;
  color: #444;
  line-height: 1.3;
  padding: .6em 1.4em .5em .8em;
  width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  margin: 0;
  border: 1px solid $main-color;
  box-shadow: 0 1px 0 1px rgba(0, 0, 0, .04);
  border-radius: .5em;
  background-color: #fff;
}

.select-css::-ms-expand {
  display: none;
}

.select-css:hover {
  border-color: #888;
}

.select-css:focus {
  border-color: #aaa;
  color: #222;
  outline: none;
}

.select-css option {
  font-weight: normal;
}
.error--valid {
  @media (min-width: 40rem) {
    grid-column: span 2;
    left: 12.75rem;
  }
  color: rgba(208, 98, 98, 0.75);
  font-style: italic;
  position: relative;
  top: -2.1rem;
  left: 0.2rem;
  font-size: 0.8rem;
  z-index: -1;
  &.value {
    top: -0.5rem;
  }
}

*[dir="rtl"] .select-css, :root:lang(ar) .select-css, :root:lang(iw) .select-css {
  background-position: left .7em top 50%, 0 0;
  padding: .6em .8em .5em 1.4em;
}

</style>
