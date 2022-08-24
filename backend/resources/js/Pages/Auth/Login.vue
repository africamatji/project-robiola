<template>
    <div>
        <v-container>
            <v-row justify="center">
                <v-col cols="12">
                    Login
                </v-col>
                <v-col cols="6">
                    <v-form
                        ref="form"
                        v-model="valid"
                        lazy-validation
                    >
                        <v-text-field
                            v-model="formData.email"
                            :rules="rules.emailRules"
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

                        <v-btn
                            color="success"
                            class="mr-4"
                            @click="submit"
                        >
                            Login
                        </v-btn>
                    </v-form>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
export default {
    name: "Login",
    data: () => ({
        formData: {
            email: '',
            password:'',
        },
        valid: true,
        rules: {
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
            ],
            required: [
                v => !!v || 'Password is required',
            ],
        },
    }),

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
                this.$inertia.post('/login', this.formData);
            }
        },
    },
}
</script>

<style scoped>

</style>
