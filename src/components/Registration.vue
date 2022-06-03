<template>
<div>
    <div v-if="!showAuthenticate" class="login_wrapper flex_row">
        <div class="background_gradient">
                <div class="login_container flex_col">
                    <div class="login_image">
                        <img src="../img/logo.png" alt="">
                    </div>
                    <div class="login_message bold">
                        <p>Create Account</p>
                    </div>
                    <div class="login_form">
                        <form>
                            <div class="input_wrap">
                                <img src="../svg/user.svg" alt="">
                                <input v-model="firstName" type="text" placeholder="First Name">
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/user.svg" alt="">
                                <input v-model="lastName" type="text" placeholder="last Name">
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/calendar-alt.svg" alt="">
                                <input v-model="birthDate" type="date" min="1918-01-01" max="2018-12-31" placeholder="Birthdate">
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/user.svg" alt="">
                                <input v-model="email" type="email" placeholder="Email">
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/lock.svg" alt="">
                                <input v-model="password" type="password" placeholder="Password">
                            </div>
                            <div class="input_wrap">
                                <img src="../svg/lock.svg" alt="">
                                <input v-model="confirmPassword" type="password" placeholder="Confirm password">
                            </div>
                            <div class="input_wrap">
                                <input v-model="joinCode" type="text" placeholder="Join code">
                            </div>
                            <div @click="closeModal" class="forgot_password rm_margin bold">
                                <p>Have an account? Login</p>
                            </div>
                            <div @click="handleAuthenticate" class="submit_button rm_margin bold">
                                <p>Create</p>
                            </div>
                        </form>
                    </div>
                </div>
        </div>
    </div>
    <Authentication v-if="showAuthenticate"/>
</div>
    
</template>
<script>
import Authentication from './Authentication.vue'
export default {
    data (){
        return {
            firstName: "",
            lastName: "",
            birthDate: "",
            email: "",
            password: "",
            confirmPassword: "",
            joinCode: "",
            showAuthenticate: false
            }
    },
    components : {Authentication},
    methods: {
        closeModal(){
            this.$emit('close')
        },
        handleAuthenticate(){
            this.showAuthenticate = !this.showAuthenticate;
        }
    },
}
</script>
<style>
    .input_wrap > input[type="text"] {
    z-index: 0;
    padding: 3%;
    padding-left: 8%;
    border-width: 1px;
    border-color: #80819445;
    border-style: solid;
    width: 100%;
    height: 40px;
    margin: 4% 0;
 }
 .input_wrap > input[type="text"]:focus {
    border: 2px solid #3eff00f0;
    border-radius: 25px;
    border-image-source: linear-gradient( #3eff00f0, #237507f0);
    border-image-slice: 1;
}
 .input_wrap > input[type="date"] {
    z-index: 0;
    padding: 3%;
    padding-left: 8%;
    border-width: 1px;
    border-color: #80819445;
    border-style: solid;
    width: 100%;
    height: 40px;
    margin: 4% 0;
 }
</style>