<template>
    <div class="main_body">
        <LoginPop v-if="loginPop" @showPop="handlePopUp" />
        <div v-if="!showReg && !resetPassword" class="login_wrapper login_body flex_col">
            <div class="background_gradient">
                <div class="login_container flex_col">
                    <div class="login_image">
                        <img src="../img/logo.png" alt="">
                    </div>
                    <div class="login_message bold">
                        <p>Welcome</p>
                    </div>
                    <div class="login_form">
                        <form>
                            <div class="container_holder flex_row">
                            <div v-show="offValidate" class="password_validCheck">
                                <div class="validCheck_row flex_row">
                                    <div class="validCheck_container">
                                        <div v-if="lowerCase" class="valid_indicator_top"></div>
                                        <div class="valid_indicator"></div>
                                    </div>
                                    <div class="validCheck_content rm_margin">
                                        <p>Lower-case</p>
                                    </div>
                                </div>
                                <div class="validCheck_row flex_row">
                                    <div class="validCheck_container">
                                        <div v-if="upperCase" class="valid_indicator_top"></div>
                                        <div class="valid_indicator"></div>
                                    </div>
                                    <div class="validCheck_content rm_margin">
                                        <p>Upper-case</p>
                                    </div>
                                </div>
                                <div class="validCheck_row flex_row">
                                    <div class="validCheck_container">
                                        <div v-if="numberData" class="valid_indicator_top"></div>
                                        <div class="valid_indicator"></div>
                                    </div>
                                    <div class="validCheck_content rm_margin">
                                        <p>Number</p>
                                    </div>
                                </div>
                                <div class="validCheck_row flex_row">
                                    <div class="validCheck_container">
                                        <div v-if="character" class="valid_indicator_top"></div>
                                        <div class="valid_indicator"></div>
                                    </div>
                                    <div class="validCheck_content rm_margin">
                                        <p>Special character</p>
                                    </div>
                                </div>
                                <div class="validCheck_row flex_row">
                                    <div class="validCheck_container">
                                        <div v-if="lengthy" class="valid_indicator_top"></div>
                                        <div class="valid_indicator"></div>
                                    </div>
                                    <div class="validCheck_content rm_margin">
                                        <p>More than 8 characters</p>
                                    </div>
                                </div>
                            </div>
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/user.svg" alt="">
                                <input type="email" placeholder="Email" v-model='email' @change="handleEmail" pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$" required>
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/lock.svg" alt="">
                                <input type="password" placeholder="Password" v-model="password" @keypress="handleChange" required>
                            </div>
                            <div @click="handleResetPassword" class="forgot_password rm_margin bold">
                                <p>Forgot password?</p>
                            </div>
                            <div @click="handleForm" class="create account rm_margin bold">
                                <p>Create Account</p>
                            </div>
                            <button @click="handlePopUp" :disabled="validEmail == false || offValidate" class="submit_button flex_row rm_margin bold">
                                <p>Login</p>
                                <div v-if="loading"  class="loading">
                                    <img src="../svg/rotate.svg" alt="">
                                </div>
                            </button>
                            <div v-show="errorMessage.length !== 0" class="error_message rm_margin">
                                <p>{{errorMessage}}</p>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
        <Registration v-if="showReg" @close="handleForm" />
        <PasswordReset v-if="resetPassword" @closeReset="handleResetPassword" />
    </div>
</template>
<script>
import Registration from './Registration.vue'
import LoginPop from './LoginPop.vue'
import PasswordReset from './PasswordReset.vue'

export default {
    data (){
        return {
            email: "",
            password: "",
            upperCase: false,
            lowerCase: false,
            character: false,
            numberData: false,
            lengthy: false,
            errorMessage: "something is wrong",
            offValidate: false,
            loading: false,
            showReg: false,
            loginPop: false,
            resetPassword: false,
            validEmail: false
        }
    },
    components : { Registration, LoginPop, PasswordReset },
    methods: {
        handleChange() {
            if(this.password.length == 0) {  
                this.errorMessage = "**Fill the password please!";  
            }

            //form input switch
            if(this.password.length > 0){
                this.offValidate = true;
            }

            // Special character
            let specialCharacter = /[!"#$%&'()*+,\-./:;<=>?@[\\\]^_`{|}~]/g;
            if(specialCharacter.test(this.password) == true){
                    this.character = true;
            }else {
                this.character = false;
            }

            // Upper case letter
            let upperCaseLetters = /[A-Z]/g;
            if(upperCaseLetters.test(this.password) == true){
                    this.upperCase = true; 
            }else {
                this.upperCase = false;
            }

            // Lower case letter
            let lowerCaseLetters = /^[a-z][a-z0-9_.]*$/;
            if(lowerCaseLetters.test(this.password) == false){
                    this.lowerCase = true;
            }else{
                 this.lowerCase = false;
            }

            // Number Validation
            let numberCase = /[0-9]/g;
            if(numberCase.test(this.password) == true){
                    this.numberData = true 
            }else {
                this.numberData = false 
            }

            //minimum password length validation  
            if(this.password.length >= 8) {  
                this.lengthy = true;
            }else {
                this.lengthy = false;
            }
            
            //maximum length of password validation  
            if(this.password.length > 15) {  
                this.passwordError = "**Password length must not exceed 15 characters";
                console.log(this.passwordError)   
                return false;  
            }
            
            if(this.upperCase && this.lowerCase && this.character && this.numberData && this.lengthy !== false){
                this.offValidate = false;
            }
        },
        handleEmail(){
            let emailVerify = /[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]/g;
            //Email test
            if(emailVerify.test(this.email) == true){
                this.validEmail = true
            }else{
                this.validEmail = false;
                this.errorMessage = "invalid email"
            }
        },
        handleValidate (){
            this.offValidate = true;
        },
        handleForm (){
            this.showReg = !this.showReg;
        },
        handlePopUp (){
            this.loginPop = !this.loginPop;
        },
        handleResetPassword (){
            this.resetPassword = !this.resetPassword;
        }

    }
}
</script>

<style>
    .main_body {
        position: relative;
        z-index: 0;
    }
    .login_body {
        z-index: 0;
    }
    .container_holder {
        position: relative;
        z-index: 0;
        width: 400px;
    }
    .password_validCheck {
        background-color: var(--text-color);
        height: fit-content;
        width: 50%;
        padding: 2%;
        bottom: -190%;
        border-radius: 5px;
        border: 1px solid #3eff00f0;
        z-index: 1;
        position: absolute;
        bottom: 0;
    }

    .validCheck_row {
        width: 100%;
        margin: 3% 0;
        align-items: center;
    }

    .validCheck_container {
        width: 15%;
        position: relative;
        z-index: 0;
    }

    .validCheck_content {
        width: 85%;
        text-align: left;
    }

    .validCheck_content > p {
        color: #fff;
        font-size: 13px;
        font-weight: 500;
    }

    .valid_indicator_top {
        width: 10px;
        height: 10px;
        border-radius: 10px;
        background-color: #8dfa6a;
        z-index: 1;
        position: absolute;
    }

    .valid_indicator {
        width: 10px;
        height: 10px;
        border-radius: 10px;
        background-color: #fff;
        z-index: 0;
    }

    .loading > img {
        width: 22px;
        margin-left: 10px;
        -webkit-animation: loading 2s infinite ease;
        animation: loading 2s infinite ease;
    }

    .error_message {
        margin: 5% 0;
    }

    .error_message > p{
        font-size: 12px;
        color: red;
        font-weight: 500;
    }

    button[disabled]{
        opacity: 0.2;
        cursor: not-allowed;
    }

    @keyframes loading {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}

</style>