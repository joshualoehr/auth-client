<template>
    <div id="login-widget-account-create-container">
        <TextInput v-for="({ key, placeholder, value, touched, error }) in fields" :key="key"
            :password="key === 'password'"
            :placeholder="placeholder"
            :value="value"
            @input="updateField(key, 'value', $event); updateField(key, 'error', false)"
            :touched="touched"
            @touched="updateField(key, 'touched', true)"
            :error="error"
            @enter="createAccount"
        />
        <button class="login-widget-content" @click="createAccount">Create account</button>
    </div>
</template>

<script>
    import TextInput from './TextInput';

    export default {
        name: 'CreateAccount',
        components: { TextInput },
        data: () => ({
            fields: [
                {
                    key: 'username',
                    placeholder: 'Username',
                    ...TextInput.defaultModel()
                },
                {
                    key: 'email',
                    placeholder: 'Email',
                    ...TextInput.defaultModel()
                },
                {
                    key: 'password',
                    placeholder: 'Password',
                    ...TextInput.defaultModel()
                },
                {
                    key: 'firstName',
                    placeholder: 'First Name',
                    ...TextInput.defaultModel()
                },
                {
                    key: 'lastName',
                    placeholder: 'Last Name',
                    ...TextInput.defaultModel()
                }
            ]
        }),
        methods: {
            updateField: function(key, attr, value) {
                this.fields.find(field => field.key === key)[attr] = value;
            },
            createAccount: function() {
                this.fields.forEach(field => {
                    this.updateField(field.key, 'touched', true);
                    if (!field.value) {
                        this.updateField(field.key, 'error', true);
                    }
                });

                if (this.fields.some(field => !field.value)) {
                    this.$emit('error', 'Missing one or more required fields.');
                } else {
                    this.$emit('error', null);
                    console.log('Attempt create account', this.fields.map(field => field.value));
                }
            }
        }
    }
</script>

<style scoped>
    #login-widget-account-create-container {
        flex-grow: 3;
        display: flex;
        flex-direction: column;
    }

    button.login-widget-content {
        flex-grow: 1;
        border-radius: 3px;
        height: 40px;
        margin: 0.8rem 0;
        cursor: pointer;
        color: white;
        background-image: linear-gradient(rgb(0, 134, 194), rgb(0, 118, 171));
        border: 1px solid rgb(0, 69, 106);
        padding: 0.4rem 0;
        font-size: 14px;
    }

    button.login-widget-content:hover {
        background-image: linear-gradient(rgb(0, 154, 222), rgb(0, 134, 194));
    }
</style>