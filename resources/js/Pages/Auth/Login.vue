<template>
    <jet-authentication-card>
        <div class="Sign-up justify-content-center text-center mt-10">Login</div>

        <p class="text-center mb-6 mt-4 description">Welcome to StockCTRL solutions <br />
            Neki text ovde neki tekst ovde neki text ovde <br />
            neki text ovde neki text ovde</p>

        <jet-validation-errors class="mb-4" />

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <jet-input placeholder="Email" id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autofocus />
            </div>

            <div class="mt-4">
                <jet-input placeholder="Password" id="password" type="password" class="mt-1 block w-full" v-model="form.password" required autocomplete="current-password" />
            </div>

            <div class="block mt-4">
                <label class="flex items-center">
                    <jet-checkbox name="remember" v-model:checked="form.remember" />
                    <span class="ml-2 text-sm text-gray-600 main-color link-main">Zapamti me</span>
                </label>
            </div>

            <div class="flex items-center justify-center mt-4">
                <inertia-link v-if="canResetPassword" :href="route('password.request')" class="text-sm text-gray-600 hover:text-gray-900 main-color link-main">
                    Forgot password?
                </inertia-link>
            </div>
            <div class="flex items-center justify-center mt-4">
                <p class="text-sm mr-1">Don’t have an account?</p>
                <inertia-link :href="route('register')" class="text-center text-sm text-gray-600 hover:text-gray-900 main-color link-main">
                    Create account
                </inertia-link>
            </div>
            <div class="flex items-center justify-center mt-4 mb-8">
                <jet-button class="" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    LOGIN
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
    import JetCheckbox from '@/Jetstream/Checkbox'
    import JetLabel from '@/Jetstream/Label'
    import JetValidationErrors from '@/Jetstream/ValidationErrors'

    export default {
        components: {
            JetAuthenticationCard,
            JetAuthenticationCardLogo,
            JetButton,
            JetInput,
            JetCheckbox,
            JetLabel,
            JetValidationErrors
        },

        props: {
            canResetPassword: Boolean,
            status: String
        },

        data() {
            return {
                form: this.$inertia.form({
                    email: '',
                    password: '',
                    remember: false
                })
            }
        },

        methods: {
            submit() {
                this.form
                    .transform(data => ({
                        ... data,
                        remember: this.form.remember ? 'on' : ''
                    }))
                    .post(this.route('login'), {
                        onFinish: () => this.form.reset('password'),
                    })
            }
        }
    }
</script>
