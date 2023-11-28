<template>
  <div class="container__form form ">
    <form  class="form__main" @submit.prevent="checkForm">

      <div class="form__item ">
        <label class="form__label">Фамилия:</label>
        <input 
        class="form__input form-control" 
        type="text"  
        :class="$v.form.lastName.$error ? 'is-invalid' : ''"
        v-model.trim="form.lastName"
        >
        <p v-if="$v.form.lastName.$error" class="invalid-feedback">*Поле обезательно для заполнения</p>
      </div>

     

      <div class="form__item">
        <label class="form__label">Имя:</label>
        <input 
        class="form__input" 
        type="text"  
        v-model.trim="form.firstName"
        :class="$v.form.firstName.$error ? 'is-invalid' : ''"
        >
        <p v-if="$v.form.firstName.$error" class="invalid-feedback">*Поле обезательно для заполнения</p>
      </div>

      <div class="form__item">
        <label class="form__label">Отчество:</label>
        <input 
        class="form__input" 
        type="text"  
        v-model.trim="form.midleName">
      </div>

      <div class="form__item">
        <label class="form__label">Дата рождения:</label>
        <input 
        class="form__input" 
        type="date"  
        :class="$v.form.data.$error ? 'is-invalid' : ''"
        v-model.trim="form.data"
        >
        <p v-if="$v.form.data.$error" class="invalid-feedback">*Поле обезательно для заполнения</p>
      </div>

      <div class="form__item">
        <label class="form__label">Номер телефона:</label>
        <input 
        placeholder="7 xxx xxx xx xx"
        class="form__input" 
        type="tel"  
        :class="$v.form.telephoneNumber.$error ? 'is-invalid' : ''"
        v-model.trim="form.telephoneNumber"
        >
        <p v-if="$v.form.telephoneNumber.$error" class="invalid-feedback">
        *Поле обезательно для заполнения, образец 7999-999-99-99 </p>
      </div>

     

      <div class="form__item">
        <label for="gender">Пол:</label>
       <div class="form__row">
          <input type="radio" id="male" name="gender" value="male" checked v-model="form.gender">
          <label for="male">Мужской</label>
       </div>
       <div class="form__row">
          <input type="radio" id="female" name="gender" value="female" v-model="form.gender">
          <label for="female">Женский</label>
       </div>
      </div>

      <div class="form__item form__item2">
            <label for="clientGroup">Группа клиентов:</label>
            <select class="form__select" id="clientGroup" name="clientGroup" 
            :class="$v.form.client.$error ? 'is-invalid' : ''"
            v-model="form.client" multiple >
              <option 
              v-for="(clients, index) in clientGroup"
              :key="index"
              :value="clients.value"
              >
              {{ clients.label }}
              </option>
            </select>
            <p v-if="$v.form.client.$error" class="invalid-feedback">*Поле обезательно для выбора</p>
      </div>

      <div class="form__item">
        <label for="attendingDoctor">Лечащий врач:</label>
        <select id="attendingDoctor" name="attendingDoctor" v-model="form.doctor">
          <option  
              v-for="(doctors, index) in doctorGroup"
              :key="index"
              :value="doctors.value"
              >
              {{ doctors.label }}
          </option>
        </select>
      </div>

      <div class="form__item">
        <div class="form__row">
            <input type="checkbox" class="form__checkbox" id="noSMS" name="noSMS" v-model="form.sms">
            <label for="noSMS">Не отправлять СМС</label>
        </div>
      </div>

      <fieldset class="form__fieldset">
        <legend>Адрес:</legend>
        <div class="form__item item2">
          <label for="zipCode">Индекс:</label>
          <input class="form__input" type="text" id="zipCode" name="zipCode" v-model="form.adress.zipCode">
        </div>
        <div class="form__item item2">
          <label for="country">Страна:</label>
          <input class="form__input" type="text" id="country" name="country" v-model="form.adress.country">
        </div>
        <div class="form__item item2">
          <label for="region">Область:</label>
          <input class="form__input" type="text" id="region" name="region" v-model="form.adress.region">
        </div>
        <div class="form__item item2">
          <label for="city">Город:</label>
          <input class="form__input" type="text" id="city" name="city"
          :class="$v.form.adress.city.$error ? 'is-invalid' : ''"
          v-model="form.adress.city">
          <p v-if="$v.form.adress.city.$error" class="invalid-feedback">*Поле обезательно для заполнения</p>
        </div>
        <div class="form__item item2">
          <label for="street">Улица:</label>
          <input class="form__input" type="text" id="street" name="street" v-model="form.adress.street">
        </div>
        <div class="form__item item2">
          <label for="house">Дом:</label>
          <input class="form__input" type="text" id="house" name="house" v-model="form.adress.house">
        </div>
      </fieldset>

      <fieldset class="form__fieldset">
        <legend>Паспорт:</legend>
        <div class="form__item item2">
          <label for="documentType">Тип документа:</label>
          <select id="documentType" name="documentType" v-model="form.passport"  :class="$v.form.passport.$error ? 'is-invalid' : ''">
            <option  v-for="(passporty, index) in passportGroup"
              :key="index"
              :value="passporty.value"
              >
              {{ passporty.label }}
            </option>
          </select>
          <p v-if="$v.form.passport.$error" class="invalid-feedback">*Поле обезательно для выбора</p>
        </div>
        <div class="form__item item2">
          <label for="passportSeries">Серия:</label>
          <input  class="form__input"  type="text" id="passportSeries" name="passportSeries" v-model="form.passportItem.passportSeries">
        </div>
        <div class="form__item item2">
          <label for="passportNumber">Номер:</label>
          <input  class="form__input"  type="text" id="passportNumber" name="passportNumber" v-model="form.passportItem.passportNumber">
        </div>
        <div class="form__item item2">
          <label for="passportIssuer">Кем выдан:</label>
          <input  class="form__input"  type="text" id="passportIssuer" name="passportIssuer" v-model="form.passportItem.passportIssuer">
        </div>
        <div class="form__item item2">
          <label for="passportIssueDate">Дата выдачи:</label>
          <input  class="form__input"  type="date" id="passportIssueDate" name="passportIssueDate"  
          :class="$v.form.passportItem.passportIssueDate.$error ? 'is-invalid' : ''"
          v-model="form.passportItem.passportIssueDate">
          <p v-if="$v.form.passportItem.passportIssueDate.$error" class="invalid-feedback">*Поле обезательно для заполнения</p>
        </div>
      </fieldset>
      <div class="form__item item3"><button class="form__button" type="submit">Отправить</button></div>
    </form>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required,numeric,minLength,maxLength  } from 'vuelidate/lib/validators'
import { isPhone } from "../assets/js/validators";
export default {
  mixins:[validationMixin],
  name: 'SingUp',
  data(){
    return{
      form:{
        lastName:"",
        firstName:"",
        midleName:"",
        data:"",
        gender:"male",
        telephoneNumber:"",
        client:[],
        doctor:"",
        sms:false,
        passport:"",
        adress:
        {
          zipCode:"",
          country:"",
          region:"",
          city:"",
          street:"",
          house:"",
        },
        passportItem:
        {
          passportSeries:"",
          passportNumber:"",
          passportIssuer:"",
          passportIssueDate:"",
        }
      },
      clientGroup:[
        {
          label:"VIP",
          value:"VIP"
        },
        {
          label:"Проблемные",
          value:"Проблемные"
        },
        {
          label:"ОМС",
          value:"ОМС"
        },
      ],
      doctorGroup:[
        {
          label:"Иванов",
          value:"Иванов"
        },
        {
          label:"Захаров",
          value:"Захаров"
        },
        {
          label:"Чернышева",
          value:"Чернышева"
        },
      ],
      passportGroup:[
        {
          label:"Паспорт",
          value:"Паспорт"
        },
        {
          label:"Свидетельствво о рождении",
          value:"Свидетельствво о рождении"
        },
        {
          label:"Вод. удостоверение",
          value:"Вод. удостоверение"
        },
      ],
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Новый клиент успешно создан')
      }
    }
  },
  validations:{
    form:{
      telephoneNumber:{required,numeric,minLength:minLength(11),maxLength:maxLength(11),isPhone},
      lastName:{required},
      firstName:{required},
      client:{required},
      data:{required},
      adress:{
        city:{required},
      },
      passport:{required},
      passportItem:{
        passportIssueDate:{required},
      },

    }
  }
}
</script>

<style scoped lang="scss">
.container__form {
  padding: 0 75px;
}

.form{
  &__select{
    border-radius: 5px;
    padding: 5px;
    border: 1px solid #000;
    &::-webkit-scrollbar {
      width: 0;
    }
  }
  &__main{
 
  }

  &__button{
    display: inline-flex;
    justify-content: center;
    align-items: center;
    padding: 16px 24px;
    border-radius: 8px;
    background: #000;
    color: #FFF;
    font-weight: 700;
  }

  &__fieldset{
    border: 1px solid #000;
    border-radius: 10px;
    padding: 20px 10px;
    max-width: 350px;
    margin-bottom: 10px;
  }

  &__row{
    flex: 1 1 auto;
    display: flex;
    align-items: center;
    gap:6px;

    
  input[type='radio']{
  position: relative;
  height: 22px;
  width: 22px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  outline: none;
}

input[type='radio']::before{
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  border: 2px solid #000;
}

input[type='radio']:checked::after{
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background-color: #000;
  transform: translate(-50%, -50%);
  visibility: visible;
}

  }

  &__item {
    position: relative;
    width: 350px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;

}
&__item2{
    align-items: flex-start;
  }
&__label {
}

&__input {
  display: inline-flex;
  align-items: center;
  padding: 5px;
  border: 1px solid #000;
  background:  #FFF;
}
.invalid-feedback{
  color: red;
  font-size: 12px;
  position: absolute;
  top: -20px;
  right: 0;
}
.is-invalid{
  border-color: red;
  color: red;
}
}
.item2{
  width: auto;
}
.item3{
  justify-content: center;
}
</style>
