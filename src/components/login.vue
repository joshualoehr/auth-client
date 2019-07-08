
<template>
    <div id="login-widget-login-container">
        <TextInput v-for="({ key, placeholder, value, touched, error }) in fields" :key="key"
            :password="key === 'password'"
            :placeholder="placeholder"
            :value="value"
            @input="updateField(key, 'value', $event); updateField(key, 'error', false)"
            :touched="touched"
            @touched="updateField(key, 'touched', true)"
            :error="error"
            @enter="login"
        />
        <button class="login-widget-content" @click="login">Sign in</button>
    </div>
</template>

<script>
    import TextInput from './TextInput';

    export default {
        name: 'login',
        components: { TextInput },
        props: {
            client_id: String
        },
        data: () => ({
            fields: [
                {
                    key: 'username',
                    placeholder: 'Email or Username',
                    ...TextInput.defaultModel()
                },
                {
                    key: 'password',
                    placeholder: 'Password',
                    ...TextInput.defaultModel()
                }
            ]
        }),
        methods: {
            getField: function(key) {
                return this.fields.find(field => field.key === key);
            },
            updateField: function(key, attr, value) {
                this.fields.find(field => field.key === key)[attr] = value;
            },
            login: function() {
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

                    const username = this.getField('username').value;
                    const password = this.getField('password').value;
                    const client_id = this.client_id;

                    fetch('/login', {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({ username, password, client_id })
                    })
                    .then(res => res.json())
                    .then(({ consent: consentGranted, id_token }) => {
                        this.$emit('authenticated', { username, consentGranted, id_token });
                    })
                    .catch(console.error);
                }
            }
        }
    }
</script>

<style scoped>
    #login-widget-login-container {
        flex-grow: 3;
        display: flex;
        flex-direction: column;
    }

    button.login-widget-content {
        height: 40px;
        border-radius: 3px;
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