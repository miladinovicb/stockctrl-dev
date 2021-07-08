<template>
    <jet-authentication-card>
        <div class="Sign-up justify-content-center text-center mt-10">Forgot password</div>

        <p class="text-center mb-10 mt-4 description">Welcome to StockCTRL solutions <br />
            Forgot your password? No problem. Just let us know your email address and we will email you a password reset link that will allow you to choose a new one
            <br />
            <inertia-link :href="route('login')" class="text-center text-sm text-gray-600 hover:text-gray-900 main-color link-main">
                or go back to Login page
            </inertia-link>
        </p>


<!--        <div class="mb-4 text-sm text-gray-600">-->
<!--            Forgot your password? No problem. Just let us know your email address and we will email you a password reset link that will allow you to choose a new one.-->
<!--        </div>-->

        <div v-if="status" class="mb-4 font-medium text-sm main-color">
            {{ status }}
        </div>

        <jet-validation-errors class="mb-4" />

        <form @submit.prevent="submit">
            <div>
                <jet-input placeholder="Email" id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autofocus />
            </div>

            <div class="flex items-center justify-center mt-6 mb-20 ">
                <jet-button :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Send Password Reset Link
                </jet-button>
            </div>
        </form>
    </jet-authentication-card>
</template>

<script>
    import JetAuthenticationCard from '@/Jetstream/AuthenticationCard'
    import JetAuthenticationCardLogo from '@/Jetstream/AuthenticationCardLogo'
    import JetButton from '@/Jetstream/Button'
    import JetInput from '@/Jetstream/Input'
    import JetLabel from '@/Jetstream/Label'
    import JetValidationErrors from '@/Jetstream/ValidationErrors'

    export default {
        components: {
            JetAuthenticationCard,
            JetAuthenticationCardLogo,
            JetButton,
            JetInput,
            JetLabel,
            JetValidationErrors
        },

        props: {
            status: String
        },

        data() {
            return {
                form: this.$inertia.form({
                    email: ''
                })
            }
        },

        methods: {
            submit() {
                this.form.post(this.route('password.email'))
            }
        }
    }
</script>
