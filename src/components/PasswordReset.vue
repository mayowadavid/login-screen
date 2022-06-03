<template lang="">
    <div class="login_wrapper flex_row">
        <div class="background_gradient">
        <div class="login_container flex_col">
            <div class="login_image">
                <img src="img/Bosque Applications.png" alt="">
            </div>
            <div class="login_message bold">
                <p>Password Reset</p>
            </div>
            <div class="login_form">
                <form>
                    <div class="input_wrap">
                    <input v-model="approvalCode" type="text" placeholder="Approval Code">
                    </div>
                    <div class="input_wrap">
                    <input v-model="password" type="text" placeholder="password">
                    </div>
                    <div class="input_wrap">
                    <input v-model="confirmPassword" type="text" placeholder="confirm password">
                </div>
                    <div @click="closeReset" class="submit_button rm_margin bold">
                        <p>Reset</p>
                    </div>
                </form>
            </div>
        </div>
        </div>
    </div>
</template>
<script>
export default {
    data (){
        return {
            approvalCode: "",
            password: "",
            confirmPassword: ""
        }
    },
    methods: {
        closeReset(){
            this.$emit("closeReset")
        }
        
    },
}
</script>
<style>
    
</style>