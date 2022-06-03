<template>
    <div @click.self="closeModal" class="login_pop_background flex_row">
        <div class="background_gradient">
            <div class="login_container flex_col">
                <div class="login_message bold">
                    <p>Which is true?</p>
                </div>
                <div class="login_form auth">
                    <form>
                        <div class="login_pop_radio flex_col">
                            <div class="pop_radio_login flex_row rm_margin">
                                <input v-model="firstSelect" type="radio" name="" id="">
                                <p>Is this your device</p>
                            </div>
                            <div class="pop_radio_login flex_row rm_margin">
                                <input v-model="secondSelect" type="radio" name="" id="">
                                <p>Is this your device</p>
                            </div>
                        </div>
                        <div class="submit_button rm_margin bold">
                            <p>Confirm</p>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            firstSelect: "",
            secondSelect: ""
            }
    },
    methods: {
        closeModal(){
            this.$emit('showPop')
        }
    },
}
</script>
<style>
    .login_pop_background {
        width: 100%;
        height: 100vh;
        position: absolute;
        z-index: 1000;
        background-color: rgba(0, 0, 0, 0.2);
    }
</style>