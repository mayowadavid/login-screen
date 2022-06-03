<template>
<div>
    <div v-if="!showQuestion" class="login_wrapper flex_row">
        <div class="background_gradient">
            <div class="login_container flex_col">
                <div class="login_image">
                    <img src="img/Bosque Applications.png" alt="">
                </div>
                <div class="login_message bold">
                    <p>Authentication Setup</p>
                </div>
                <div class="login_form auth">
                    <form>
                        <div class="input_wrap">
                            <input v-model="verifyNumber" type="text" placeholder="xxx-xxx-xxxx">
                        </div>
                        <div class="authentication_message rm_margin">
                            <p>*Standard SMS and Data rate Rates will apply</p>
                        </div>
                        <div class="message_check flex_row rm_margin bold">
                            <input type="checkbox" name="" id="">
                            <p>I cannot receive text messages</p>
                        </div>
                        <div @click="handleChange" class="submit_button rm_margin bold">
                            <p>Confirm</p>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
    <SecurityQuestion v-if="showQuestion" />
</div>
</template>
<script>
import SecurityQuestion from './SecurityQuestion.vue'
export default {
    data(){
        return {
            verifyNumber: "",
            showQuestion: false
            }
    },
    components: {
        SecurityQuestion
    },
    methods: {
        handleChange (){
            this.showQuestion= !this.showQuestion;
        }
    },
}
</script>
<style>
    
</style>