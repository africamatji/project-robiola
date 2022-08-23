<template>
    <div>
        <v-container>
            <v-row justify="center">
                <v-col cols="12">
                    Register
                </v-col>
                <v-col cols="6">
                    <v-form
                        ref="form"
                        v-model="valid"
                        lazy-validation
                    >
                        <v-text-field
                            v-model="formData.name"
                            :rules="rules.name"
                            label="Name"
                            required
                        ></v-text-field>

                        <v-text-field
                            v-model="formData.email"
                            :rules="rules.email"
                            label="E-mail"
                            required
                        ></v-text-field>

                        <v-text-field
                            v-model="formData.password"
                            :rules="rules.required"
                            label="Password"
                            type="password"
                            required
                        ></v-text-field>

                        <v-text-field
                            v-model="formData.password_confirmation"
                            :rules="rules.required"
                            label="Confirm Password"
                            type="password"
                            required
                        ></v-text-field>
                        <v-checkbox
                            v-model="acceptTerms"
                            label="Accept Terms & Conditions"
                            :rules="requiredCheckBox"
                        ></v-checkbox>
                        <v-alert type="success" v-if="submitErrors.length > 0">
                            <span v-for="error in submitErrors">
                                {{ error }}
                            </span>
                        </v-alert>
                        <v-btn
                            color="success"
                            class="mr-4"
                            @click="submit"
                        >
                            Register
                        </v-btn>
                    </v-form>
                </v-col>
            </v-row>
        </v-container>
    </div>

</template>

<script>
export default {
    name: "Register",
    data: () => ({
        formData: {
            name: '',
            email: null,
            password: '',
            password_confirmation: '',
        },
        valid: false,
        acceptTerms: false,
        submitErrors: [],
        rules: {
            name: [
                v => !!v || 'Name is required',
                v => (v && v.length >= 2) || 'Name must be more than 2 characters',
            ],
            email: [
                v => !!v || 'E-mail is required',
                v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
            ],
            required: [
                v => !!v || 'Required',
            ],
        },
    }),
    computed:{
        requiredCheckBox () {
            return [ this.acceptTerms || 'Please accept Terms' ];
        }
    },
    methods: {
        validate () {
            this.$refs.form.validate()
        },
        reset () {
            this.$refs.form.reset()
        },
        resetValidation () {
            this.$refs.form.resetValidation()
        },
        submit () {
            if (this.$refs.form.validate()) {
                if (this.formData.password !== this.formData.password_confirmation) {
                    console.log('password mismatch');
                    this.submitErrors.push('Password mismatch');
                    return;
                }
                this.$inertia.post('/register', this.formData);
            }
        },
    },
}
</script>

<style scoped>

</style>
