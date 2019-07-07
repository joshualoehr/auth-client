
<template>
    <div id="login-widget-login-container">
        <TextInput
            placeholder="Email or Username"
            :value="username.value"
            @input="username.value = $event; username.error = false"
            :touched="username.touched"
            @touched="username.touched = true"
            :error="username.error"
            @enter="login"
        />
        <TextInput
            :password="true"
            placeholder="Password"
            :value="password.value"
            @input="password.value = $event; password.error = false"
            :touched="password.touched"
            @touched="password.touched = true"
            :error="password.error"
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
        data: () => ({
            username: {
                value: '',
                touched: false,
                error: false
            },
            password: {
                value: '',
                touched: false,
                error: false
            }
        }),
        methods: {
            login: function() {
                const { username, password } = this;

                this.username.touched = true;
                this.password.touched = true;

                if (!username.value) {
                    this.username.error = true;
                }
                
                if (!password.value) {
                    this.password.error = true;
                }

                if (!username.value || !password.value) {
                    this.$emit('error', 'Missing one or more required fields.');
                    return;
                } else {
                    this.$emit('error', null);
                    console.log('Attempt login:', username, password);
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
        flex-grow: 1;
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