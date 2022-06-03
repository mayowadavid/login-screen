<template >
    <div class="login_wrapper flex_row">
        <div class="background_gradient">
        <div class="login_container flex_col">
            <div class="login_message bold">
                <p>Security Questions</p>
            </div>
            <div class="login_form">
                <form>
                <div class="random_questions bold">
                    <p>Random questions</p>
                    <input v-model="firstQuestion" type="text" placeholder="xxx-xxx-xxxx">
                </div>
                <div class="random_questions bold">
                    <p>Random questions</p>
                    <input v-model="secondQuestion" type="text" placeholder="xxx-xxx-xxxx">
                </div>
                <div class="random_questions bold">
                    <p>Random questions</p>
                    <input v-model="thirdQuestion" type="text" placeholder="xxx-xxx-xxxx">
                </div>    
                    <div class="submit_button rm_margin bold">
                        <p>0/3 Answered</p>
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
            firstQuestion: "",
            secondQuestion: "",
            thirdQuestion: ""
        }
    }
}
</script>
<style lang="">
    
</style>