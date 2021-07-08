<template>
    <jet-authentication-card>

        <jet-validation-errors class="mb-4" />
        <div class="Sign-up justify-content-center text-center mt-10">Sign up</div>
        <p class="text-center mb-6 mt-4 description">Welcome to StockCTRL solutions <br />
Neki text ovde neki tekst ovde neki text ovde <br />
neki text ovde neki text ovde</p>
        <form @submit.prevent="submit">
            <div>
                <jet-input placeholder="First name" id="first_name" type="text" class="mt-1 block w-full" v-model="form.first_name" required autofocus autocomplete="name" />
            </div>

            <div>
                <jet-input placeholder="Last name" id="last_name" type="text" class="mt-1 block w-full" v-model="form.last_name" required autofocus autocomplete="name" />
            </div>


            <div class="mt-4">
                <jet-input placeholder="Email" id="email" type="email" class="mt-1 block w-full" v-model="form.email" required />
            </div>

            <div class="mt-4">
                <jet-input placeholder="Password" id="password" type="password" class="mt-1 block w-full" v-model="form.password" required autocomplete="new-password" />
            </div>

            <div class="mt-4">
                <jet-input placeholder="Re - enter password" id="password_confirmation" type="password" class="mt-1 block w-full" v-model="form.password_confirmation" required autocomplete="new-password" />
            </div>

            <div class="mt-4" v-if="$page.props.jetstream.hasTermsAndPrivacyPolicyFeature">
                <jet-label for="terms">
                    <div class="flex items-center">
                        <jet-checkbox name="terms" id="terms" v-model:checked="form.terms" />

                        <div class="ml-2">
                            I agree to the <a target="_blank" :href="route('terms.show')" class="underline text-sm text-gray-600 hover:text-gray-900">Terms of Service</a> and <a target="_blank" :href="route('policy.show')" class="underline text-sm text-gray-600 hover:text-gray-900">Privacy Policy</a>
                        </div>
                    </div>
                </jet-label>
            </div>

            <div class="flex items-center justify-center  mt-8">


                <jet-button class="text-center content-center" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    SIGN UP
                </jet-button>
            </div>

            <div class="flex items-center justify-center mt-4 mb-6">
                <inertia-link :href="route('login')" class="text-center text-sm text-gray-600 hover:text-gray-900 main-color link-main">
                    Already registered?
                </inertia-link>
            </div>
        </form>
    </jet-authentication-card>
</template>

<script>
    import JetAuthenticationCard from '@/Jetstream/AuthenticationCard'
    import JetAuthenticationCardLogo from '@/Jetstream/AuthenticationCardLogo'
    import JetButton from '@/Jetstream/Button'
    import JetInput from '@/Jetstream/Input'
    import JetCheckbox from "@/Jetstream/Checkbox";
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

        data() {
            return {
                form: this.$inertia.form({
                    first_name: '',
                    last_name: '',
                    email: '',
                    password: '',
                    password_confirmation: '',
                    terms: false,
                })
            }
        },

        methods: {
            submit() {
                this.form.post(this.route('register'), {
                    onFinish: () => this.form.reset('password', 'password_confirmation'),
                })
            }
        }
    }
</script>
