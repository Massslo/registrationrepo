<template>

    <div>
        <form @submit.prevent="checkForm">
<!--            <p v-if="errors.length">-->
<!--                <b>Пожалуйста, исправьте следующие ошибки:</b>-->
<!--            <ul>-->
<!--                <li v-for="error in errors" :key="error">{{ error }}</li>-->
<!--            </ul>-->
<!--            </p>-->
            <p class="pagename">
              Регистрация
            </p>

          <div>
            <p>
                <label for="email">Почта *</label>

                <input  @input="validateEmail"  type="text" name="email" id="email"  v-model="email" placeholder="Введите почту" />
              <i class="fa fa-envelope-o" aria-hidden="true"></i>
          <p class="error-message" v-if="emailError">{{ emailError }}</p>
            </p>
    </div>
            <p class="password-input relative-position">
                <label for="password">Пароль *</label>
                <input id="password" v-model="password" :type="showPassword ? 'text' : 'password'" placeholder="Пароль" />
              <i class="fa fa-lock" aria-hidden="true"></i>
              <i class="fa fa-eye"  @click="togglePasswordVisibility"></i>
            <p  class="error-message"  v-if="passwordError">{{ passwordError }}</p>
            </p>

            <p class="password-input relative-position">
                <label for="ConfirmPassword">Повтор пароля *</label>
                <input id="cpassword" v-model="confirmPassword" :type="showConfirmPassword ? 'text' : 'password'" placeholder="Повтор пароля" />
              <i class="fa fa-lock" aria-hidden="true"></i>
              <i class="fa fa-eye" @click="toggleConfirmPasswordVisibility"></i>
                            <p class="error-message"  v-if="confirmPasswordError" >{{ confirmPasswordError }}</p>
            </p>

            <p>
                <label for="phone">Телефон *</label>
                <input type="text" name="phone" id="phone" v-model="phone" placeholder="Введите номер телефона" />
              <i class="fa fa-phone" aria-hidden="true"></i>
                            <p  class="error-message"  v-if="phoneError">{{ phoneError }}</p>
            </p>

            <p>
                <label for="surname">Фамилия *</label>
                <input type="text" name="surname" id="surname" v-model="surname" placeholder="Введите фамилию" />
                            <p  class="error-message"  v-if="surnameError">{{ surnameError }}</p>
            </p>

            <p>
                <label for="firstName">Имя *</label>
                <input type="text" name="firstName" id="firstName" v-model="firstName" placeholder="Введите имя" />
                            <p class="error-message"  v-if="firstNameError">{{ firstNameError }}</p>
            </p>

            <p>
                <label for="patronymic">Отчество *</label>
                <input type="text" name="patronymic" id="patronymic" v-model="patronymic" placeholder="Введите отчество" />
                             <p class="error-message"  v-if="patronymicError">{{ patronymicError }}</p>
            </p>









            <p>
                <label for="movie">Типы услуг</label>
                <select name="movie" id="service" v-model="movie">
                    <option selected value="1">Ремонт квартир</option>
                    <option value="2">Ремонт офисов</option>
                    <option value="3">Дизайн интерьера</option>
                    <option value="4">Реставрация помещений</option>
                    <option value="5">Отделка помещений</option>
                </select>
            </p>

            <p>
                <label for="wishes">Ваши пожелания</label>
                <input type="text" name="wishes" id="wishes" v-model="wishes" placeholder="Введите ваши пожелания" />
           
                <i class="fa fa-info-circle" @mouseover="handleTooltipShow" @mouseout="handleTooltipHide"></i>
                <span class="tooltip" v-show="showTooltip">Расскажите, какой ремонт вы планируете</span>
            </p>

            <p>
                <label>Выберите виды работ, которые вас интересуют</label>
            </p>
            <div class="checkbox-group">
                <div class="checkbox-row">
                    <input type="checkbox" id="painting" v-model="painting" value="Покраска и обои"/>
                    <label for="painting">Покраска и обои</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="tiles" v-model="tiles" value="Плитка и полы" />
                    <label for="tiles">Плитка и полы</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="construction" v-model="construction" value="Строительство и перепланировка" />
                    <label for="construction">Строительство и перепланировка</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="electricity" v-model="electricity" value="Электрика и освещение" />
                    <label for="electricity">Электрика и освещение</label>
                </div>
            </div>


            <p>
                <label>Какой стиль интерьера вас интересует?</label>
            </p>



            <div class="radio-group">
                <div class="radio-row">
                    <input type="radio" id="modern" value="Современный" v-model="interiorStyle" />
                    <label for="modern">Современный</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="classic" value="Классический" v-model="interiorStyle" />
                    <label for="classic">Классический</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="eclectic" value="Эклектика" v-model="interiorStyle" />
                    <label for="eclectic">Эклектика</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="minimalism" value="Минимализм" v-model="interiorStyle" />
                    <label for="minimalism">Минимализм</label>
                </div>
            </div>

            <p>
                <label for="photo">Приложите фотографии помещения</label>
                <input type="file" name="photo" id="photo" accept="image/*" @change="handleFileUpload" />
            <p class="error-message"  v-if="uploadedFileError">{{ uploadedFileError }}</p>
            </p>

            <div class="checkbox-row">
                <div class="checkbox-wrapper">
                    <input type="checkbox" id="agreement" v-model="agreement" />
                    <label for="agreement" class="agree">Я прочитал и согласен с условиями использования сайта, включая политику конфиденциальности и правила обработки персональных данных</label>
                </div>
            </div>

            <p>
                <button type="submit" :disabled="isFormValid">Зарегистрироваться</button>
            </p>
          <div class="link">
            <p>Уже есть аккаунт?
            <router-link to="/Login">Войти</router-link>
            </p>
          </div>
<!--            <h3>Данные в хранилище:</h3>-->
<!--            <span>Фамилия: {{ register.surname }}</span><br>-->
<!--            <span>Имя: {{ register.firstName }}</span><br>-->
<!--            <span>Отчество: {{ register.patronymic }}</span><br>-->
<!--            <span>Почта: {{ register.email }}</span><br>-->
<!--            <span>Типы услуг: {{ register.movie }}</span><br>-->
<!--            <span>Пароль: {{ register.password }}</span><br>-->
<!--            <span>Повтор пароля: {{ register.confirmPassword }}</span><br>-->
<!--            <span>Телефон: {{ register.phone }}</span><br>-->
<!--            <span>Ваши пожелания: {{ register.wishes }}</span><br>-->
<!--            <span>Файл: {{ register.uploadedFile }}</span><br>-->
<!--            <h4>Выберите виды работ, которые вас интересуют:</h4>-->
<!--            <span>Строительство и перепланировка: {{ register.construction }}</span><br>-->
<!--            <span>Покраска и обои: {{ register.painting }}</span><br>-->
<!--            <span>Плитка и полы: {{ register.tiles }}</span><br>-->
<!--            <span>Электрика и освещение: {{ register.electricity }}</span><br>-->

<!--            <h4>Выберите виды работ, которые вас интересуют:</h4>-->
<!--            <span>{{ register.interiorStyle }}</span><br>-->






        </form>
    </div>
</template>

<script>
import {computed, inject, ref, toRefs, watch} from 'vue';
import { mask } from 'vue-the-mask';
import  { useRegisterStore } from '../stores/RegisterStore';
import { useRouter } from 'vue-router';


export default {
    directives: {
        mask
    },
    setup() {
        const router = useRouter();
        const register = useRegisterStore();
        const isFormValid = computed(() => {
            return (
                !email.value ||
                !password.value ||
                !confirmPassword.value ||
                !phone.value ||
                !surname.value ||
                !firstName.value ||
                !patronymic.value ||
                !agreement.value ||
                emailError.value !== '' ||
                passwordError.value !== '' ||
                confirmPasswordError.value !== '' ||
                phoneError.value !== '' ||
                surnameError.value !== '' ||
                firstNameError.value !== '' ||
                patronymicError.value !== ''||
                uploadedFileError.value !==''
            );
        });


        const agreement = ref(false);
        const uploadedFile = ref(null);
        const email = ref('');
        const movie = ref('');
        const errors = ref([]);
        const password = ref('');
        const confirmPassword = ref('');
        const showPassword = ref(false);
        const showConfirmPassword = ref(false);
        const surname = ref('');
        const firstName = ref('');
        const patronymic = ref('');
        const phone = ref('');
        const wishes = ref('');
        const showTooltip = ref(false);
        const interiorStyle = ref('');
        const painting =  ref(false);
        const tiles =  ref(false);
        const construction =  ref(false);
        const electricity =  ref(false);


        const emailError = ref('');
        const passwordError = ref('');
        const confirmPasswordError = ref('');
        const phoneError = ref('');
        const surnameError = ref('');
        const firstNameError = ref('');
        const patronymicError = ref('');
        const uploadedFileError = ref('');



        // Функция валидации email
        const validateEmail = () => {
            errors.value = [];

            if (!email.value) {
                emailError.value = 'Введите вашу электронную почту.';
              document.getElementById("email").style.borderColor = "red";
            } else if (!email.value.match(/^[^\s@]+@[^\s@]+\.[^\s@]+$/)) {
                emailError.value = 'Введите корректный адрес электронной почты.';
              document.getElementById("email").style.borderColor = "red";
            } else {
                emailError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
              document.getElementById("email").style.borderColor = "#8DD3BB";
            }
        };

        // Прослушивание изменений в поле email и запуск функции валидации
        watch(email, () => {
            validateEmail();
        });


        // Функция валидации пароля

        const validatePassword = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!password.value) {
                passwordError.value = 'Введите пароль.';
              document.getElementById("password").style.borderColor = "red";
            } else if (password.value.length < 8) {
                passwordError.value = 'Пароль должен содержать не менее 8 символов.';
              document.getElementById("password").style.borderColor = "red";
            } else if (!/[A-Z]/.test(password.value) && !/[А-Я]/.test(password.value)) {
              document.getElementById("password").style.borderColor = "red";
                passwordError.value = 'Пароль должен содержать хотя бы одну заглавную букву.';
            } else if (!/[a-z]/.test(password.value) && !/[а-я]/.test(password.value)) {
              document.getElementById("password").style.borderColor = "red";
                passwordError.value = 'Пароль должен содержать хотя бы одну строчную букву.';
            } else if (!/\d/.test(password.value)) {
              document.getElementById("password").style.borderColor = "red";
                passwordError.value = 'Пароль должен содержать хотя бы одну цифру.';
            } else if (!/[!@#$%^&*(),.?":{}|<>]/.test(password.value)) {
              document.getElementById("password").style.borderColor = "red";
                passwordError.value = 'Пароль должен содержать хотя бы один специальный символ(!@#$%^&*(),.?":{}|<>).';
            } else if (confirmPassword.value !== '' && confirmPassword.value !== password.value) {
              document.getElementById("password").style.borderColor = "red";
              passwordError.value = 'Пароли не совпадают.';
            } else {
                passwordError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
              document.getElementById("password").style.borderColor = "#8DD3BB";
            }
        };

        // Прослушивание изменений в поле пароля и запуск функции валидации
        watch(password,validatePassword);

        // Функция валидации повторного пароля
        const validateConfirmPassword = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!confirmPassword.value) {
              document.getElementById("cpassword").style.borderColor = "red";
                confirmPasswordError.value = 'Введите повторный пароль.';
            } else if (confirmPassword.value !== password.value) {
              document.getElementById("cpassword").style.borderColor = "red";
                confirmPasswordError.value = 'Пароли не совпадают.';
            } else if (!password.value) {
              document.getElementById("cpassword").style.borderColor = "red";
                confirmPasswordError.value = 'Введите пароль.';
            } else {
              document.getElementById("cpassword").style.borderColor = "#8DD3BB";
                confirmPasswordError.value = ''; // Очистка всех сообщений об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле повторного пароля и запуск функции валидации
        watch(confirmPassword, validateConfirmPassword
        );


        // Функция валидации телефона
        const validatePhone = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!phone.value) {
              document.getElementById("phone").style.borderColor = "red";
                phoneError.value = 'Введите ваш номер телефона.';
            } else {
                const phoneRegex = /^\+7\d{10}$/;
                if (!phoneRegex.test(phone.value)) {
                  document.getElementById("phone").style.borderColor = "red";
                    phoneError.value = 'Введите корректный номер телефона в формате +7 (999) 999-9999.';
                } else {
                  document.getElementById("phone").style.borderColor = "#8DD3BB";
                    phoneError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
                }
            }
        };

        // Прослушивание изменений в поле телефона и запуск функции валидации
        watch(phone, () => {
            validatePhone();
        });

        // Функция валидации фамилии
        const validateSurname = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!surname.value) {
              document.getElementById("surname").style.borderColor = "red";
                surnameError.value = 'Введите вашу фамилию.';
            } else if (surname.value.length < 2 || surname.value.length > 50) {
              document.getElementById("surname").style.borderColor = "red";
                surnameError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(surname.value)) {
              document.getElementById("surname").style.borderColor = "red";
                surnameError.value = 'Фамилия не должна содержать цифры.';
            } else {
              document.getElementById("surname").style.borderColor = "#8DD3BB";
                surnameError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле фамилии и запуск функции валидации
        watch(surname, () => {
            validateSurname();
        });

        // Функция валидации имени
        const validateFirstName = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!firstName.value) {
              document.getElementById("firstName").style.borderColor = "red";
                firstNameError.value = 'Введите ваше имя.';
            } else if (firstName.value.length < 2 || firstName.value.length > 50) {
              document.getElementById("firstName").style.borderColor = "red";
                firstNameError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(firstName.value)) {
              document.getElementById("firstName").style.borderColor = "red";
                firstNameError.value = 'Имя не должно содержать цифры.';
            } else {
              document.getElementById("firstName").style.borderColor = "#8DD3BB";
                firstNameError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле имени и запуск функции валидации
        watch(firstName, () => {
            validateFirstName();
        });

        // Функция валидации отчества
        const validatePatronymic = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!patronymic.value) {
              document.getElementById("patronymic").style.borderColor = "red";
                patronymicError.value = 'Введите ваше отчество.';
            } else if (patronymic.value.length < 2 || patronymic.value.length > 50) {
              document.getElementById("patronymic").style.borderColor = "red";
                patronymicError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(patronymic.value)) {
              document.getElementById("patronymic").style.borderColor = "red";
                patronymicError.value = 'Отчество не должно содержать цифры.';
            } else {
              document.getElementById("patronymic").style.borderColor = "#8DD3BB";
                patronymicError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле отчества и запуск функции валидации
        watch(patronymic, () => {
            validatePatronymic();
        });




        const checkForm = (event) => {


            // Установите значения полей формы в хранилище
            // register.setUploadedFile(uploadedFile.value);
            register.setEmail(email.value);
            register.setPassword(password.value);
            register.setConfirmPassword(confirmPassword.value);
            register.setPhone(phone.value);
            register.setSurname(surname.value);
            register.setFirstName(firstName.value);
            register.setPatronymic(patronymic.value);
            register.setMovie(movie.value);
            register.setWishes(wishes.value);
            register.setInteriorStyle(interiorStyle.value);
            register.setPainting(painting.value);
            register.setTiles(tiles.value);
            register.setConstruction(construction.value);
            register.setElectricity(electricity.value);
            register.setAgreement(agreement.value);


            // Если проверки прошли успешно, выполните отправку данных формы
            // Например, отправьте запрос на сервер с данными формы
            console.log('Данные отправлены:', {
                surname: surname.value,
                firstName: firstName.value,
                patronymic: patronymic.value,
                email: email.value,
                movie: movie.value,
                phone: phone.value, // Добавили номер телефона к данным для отправки
                password: password.value,
                confirmPassword: confirmPassword.value
            });

            // Очистите поля формы после отправки
            surname.value = '';
            firstName.value = '';
            patronymic.value = '';
            email.value = '';
            movie.value = '';
            password.value = '';
            confirmPassword.value = '';
            showPassword.value = false;
            phone.value = '';
            wishes.value ='';
            interiorStyle.value = '';
            painting.value = false;
            tiles.value = false;
            construction.value = false;
            electricity.value = false;
            agreement.value = false;
            emailError.value = '';
            passwordError.value = '' ;
            confirmPasswordError.value = '' ;
            phoneError.value = '' ;
            surnameError.value = '' ;
            firstNameError.value = '' ;
            patronymicError.value = '';
            // Перенаправьте пользователя на другую страницу
            router.push('/');

            // Проверьте uploadedFile на наличие файла перед отправкой формы
            //         if (!uploadedFile.value) {
            //             errors.value.push('Загрузите фотографию.');
            //         }
            // Другие проверки...
            // if (!email.value) {
            //     errors.value.push('Введите вашу электронную почту.');
            // }
            // if (!surname.value) {
            //     errors.value.push('Введите вашу фамилию.');
            // }
            //
            // if (!firstName.value) {
            //     errors.value.push('Введите ваше имя.');
            // }
            //
            // if (!patronymic.value) {
            //     errors.value.push('Введите ваше отчество.');
            // }
            // if (!agreement.value) {
            //     errors.value.push('Согласитесь с условием');
            // }
            // Другие проверки...
        };

        const togglePasswordVisibility = () => {
            showPassword.value = !showPassword.value;
        };

        const toggleConfirmPasswordVisibility = () => {
            showConfirmPassword.value = !showConfirmPassword.value;
        };

        const handleTooltipShow = () => {
            showTooltip.value = true;
        };

        const handleTooltipHide = () => {
            showTooltip.value = false;
        };

        const handleFileUpload = (event) => {
            const file = event.target.files[0];

            // Проверяем формат файла
            const allowedFormats = ['image/png', 'image/jpeg', 'image/gif', 'image/bmp'];
            if (file && !allowedFormats.includes(file.type)) {
                uploadedFileError.value = 'Формат файла должен быть PNG, JPEG, GIF или BMP.';
            } else {
                uploadedFileError.value = ''; // Очистка сообщения об ошибке, если валидация успешна

                // Если формат файла допустимый, сохраняем его в FormData и передаем в хранилище
                const formData = new FormData();
                formData.append('photo', file); // 'photo' - это имя поля файла, которое ожидается на бэкенде
                // Сохраняем объект FormData в хранилище
                register.setUploadedFile(formData);
            }
        };





        return {
            surname,
            firstName,
            patronymic,
            email,
            movie,
            errors,
            checkForm,
            password,
            confirmPassword,
            showPassword,
            showConfirmPassword,
            togglePasswordVisibility,
            toggleConfirmPasswordVisibility,
            phone, // Добавили переменную для хранения номера телефона
            wishes,
            showTooltip,
            handleTooltipShow,
            handleTooltipHide,
            interiorStyle,
            uploadedFile,
            handleFileUpload,
            agreement,
            painting,
            tiles,
            construction,
            electricity,
            isFormValid,
            register,
            validateEmail,
            validateConfirmPassword,
            validatePassword,
            validatePhone,
            validateSurname,
            validateFirstName,
            validatePatronymic,
            emailError,
            passwordError,
            confirmPasswordError,
            phoneError,
            surnameError,
            firstNameError,
            patronymicError,
            uploadedFileError,



        };
    },
};
</script>

<style scoped>
/* Стили для формы */

.pagename{
  font-size: x-large;
  font-weight: bolder;
  text-align: center;
  padding: 30px;
}

.link{
  text-align: center;
}

a {
  font-weight: 500;
  color: #9eada2;
  text-decoration: inherit;
  transition: 0.3s;
}
a:hover {
  color: #292f2e;
  transition: 0.3s;
}

form {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
}

select:focus{
  outline: 0;
  border: 2px solid #8DD3BB;
  transition: 0.2s ease-in-out;
}

p {
    margin-bottom: 15px;
    font-family: 'Arial';

}

option{
  border: 2px solid #D1D1D1;
  width: 430px;
  height: 449.81px;

  transition: 0.2s ease-in-out;
}

label {
    display: block;
  margin-bottom: 5px;
  font-family: 'Arial';
  align-items: center;
}

.checkbox-group {
    display: flex;
    flex-wrap: wrap;
    border: 0px solid #ccc; /* Толщина, стиль и цвет рамки */
    padding: 10px; /* Добавление внутренних отступов для рамки */
    border-radius: 9.96px; /* Закругление углов рамки */
    margin-bottom: 30px;
    width: 430px;
    height: 103px;
    box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
}

.checkbox-row {
    flex: 0 0 50%; /* Две колонки */
    margin-bottom: 10px;

}

input[type="checkbox"]{
  float: left;
  margin-right: 10px;
}

input[type="radio"]{
  float: left;
  margin-right: 10px;
  margin-bottom: 15px;
}


.radio-group {
  display: flex;
  flex-wrap: wrap;
  border: 0px solid #ccc; /* Толщина, стиль и цвет рамки */
  padding: 10px; /* Добавление внутренних отступов для рамки */
  margin-bottom: 30px;
  border-radius: 9.96px; /* Закругление углов рамки */
  width: 430px;
  height: 180px;
  box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
}

.radio-row {
 padding-top: 7px;
  flex: 100%; /* Две колонки */
    align-items: center; /* Выравниваем элементы по вертикали по центру */
  border: 1px solid;
  border-color: transparent transparent #ccc transparent;
  overflow: hidden;
}
.checkbox-wrapper {
  flex: 0 0 50%;
    align-items: center;
  padding-bottom: 10px;
  padding-top: 10px;
}

.checkbox-wrapper input {
   margin-top: 0px; /* Расстояние между чекбоксом и текстом */

}

.agree{
  padding-left: 50px;
  text-align: left;
}


.error-message {
    color: red; /* Устанавливаем красный цвет для текста ошибки */
  font-size: small;
  margin-top: 5px;
}

button[type="submit"]:disabled{
  width: 429px;
  height: 48px;
  padding: 8px;
  border:0px;
  border-radius: 22px;
  gap: 4px;
  background-color: #BDCAC6;
  text-color: #112211;
  font-family: 'Arial';
  font-size: 18px;
  font-weight: 600;
  line-height: 22px;
  letter-spacing: 0em;
}

input[type=file]{
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
  width: 430px;
  color: grey;
}

input[type=file]::file-selector-button {
  margin-right: 10px;
  border: 0px;
  background: #8DD3BB;
  padding: 10px 20px;
  border-radius: 5px;
  color: black;
  cursor: pointer;
  transition: background 0.1s ease-in-out;
}

input[type=file]::file-selector-button:hover {
  background: #7FB5B5;
}

button[type="submit"]{
  width: 429px;
  height: 48px;
  padding: 8px;
  border:0px;
  border-radius: 22px;
  gap: 4px;
  background-color: #8DD3BB;
  text-color: #112211;
  font-family: 'Arial';
  font-size: 18px;
  font-weight: 600;
  line-height: 22px;
  letter-spacing: 0em;
  transition: background 0.3s ease-in-out;
}

button[type="submit"]:hover:enabled{
  width: 429px;
  height: 48px;
  padding: 8px;
  border:0px;
  border-radius: 22px;
  gap: 4px;
  background-color: #7FB5B5;
  text-color: #112211;
  font-family: 'Arial';
  font-size: 18px;
  font-weight: 600;
  line-height: 22px;
  letter-spacing: 0em;
  transition: background 0.3s ease-in-out;
}

input[type="text"]{
  border: 2px solid #D1D1D1;
  width: 430px;
  height: 49.81px;
  border-radius: 9.96px;
  font-size: 16px;
  font-weight: 400;
  line-height: 19px;
  letter-spacing: 0em;
  text-align: left;
  padding-left: 20px;
  transition: 0.2s ease-in-out;
}

#email{
  padding-left: 40px;
}

#password{
  padding-left: 40px;
}

#cpassword{
  padding-left: 40px;
}

#phone{
  padding-left: 40px;
}

input[name="firstName"]{
  margin-bottom: 20px;
}

input[name="surname"]{
  margin-bottom: 20px;
}

input[name="patronymic"]{
  margin-bottom: 20px;
}

select{
  margin-bottom: 20px;
}


input[type="text"]:focus{
  outline: 0;
  border: 2px solid #8DD3BB;
  transition: 0.2s ease-in-out;
}


input[type="password"]{
  border: 2px solid #D1D1D1;
  width: 430px;
  height: 49.81px;
  border-radius: 9.96px;
  font-size: 16px;
  font-weight: 400;
  line-height: 19px;
  letter-spacing: 0em;
  text-align: left;
  padding-left: 40px;
}

input[type="password"]:focus{
  outline: 0;
  border: 2px solid #8DD3BB;
  transition: 0.2s ease-in-out;
}



#service{
  border: 1px solid #D1D1D1;
  width: 430px;
  height: 49.81px;
  top: 420.89px;
  left: 506px;
  border-radius: 9.96px;
  font-size: 16px;
  font-weight: 400;
  line-height: 19px;
  letter-spacing: 0em;
  text-align: left;
}

input[type="checkbox"]{
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #999;
  border-radius: 6px;
  outline: none;
  transition: background-color 0.1s ease-in-out;
}
input[type="checkbox"]:checked::before {
  content: '\2714';
  display: block;
  text-align: center;
  font-size: 16px;
  line-height: 18px;
  color: white;
}

input[type="checkbox"]:checked {
  background-color: #8DD3BB;
  border: 0px;
}

input[type="radio"]{
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #999;
  border-radius: 60px;
  outline: none;
  transition: background-color 0.1s ease-in-out;
}
input[type="radio"]:checked::before {
  content: "\25CF";
  display: block;
  text-align: center;
  font-size: 16px;
  line-height: 18px;
  color: white;
}


input[type="radio"]:checked {
  background-color: #8DD3BB;
  border: 0px;
}

i {
  position: relative;
  top: -35px;
  left: 15px;
}

.fa-eye{
  position: relative;
  top: -35px;
  left: 385px;
}

.fa-info-circle {
  position: relative;
  top: -35px;
  left: 395px;
}

</style>

