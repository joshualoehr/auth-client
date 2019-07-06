
<template>
    <div id="login-widget-login-container">
        <input 
            class="login-widget-content" 
            type="text" 
            placeholder="Email or Username" 
            :class="{ error: errors.username }"
            @input="$emit('username-changed', $event.target.value)"
            @keyup.enter="$emit('login-attempt')"
        />
        <input 
            class="login-widget-content" 
            type="password" 
            placeholder="Password" 
            :class="{ error: errors.password }"
            @input="$emit('password-changed', $event.target.value)"
            @keyup.enter="$emit('login-attempt')"
        />
        <button class="login-widget-content" @click="$emit('login-attempt')">Sign in</button>
    </div>
</template>

<script>
    export default {
        name: 'login',
        props: {
            errors: {
                type: Object,
                default: () => ({
                    username: false,
                    password: false
                })
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

    #login-widget-login-container > .login-widget-content {
        flex-grow: 1;
    }

    input.login-widget-content {
        margin: 0.4rem 0;
        border-radius: 3px;
    }

    input.login-widget-content {
        padding: 0 0.8rem;
        border: 1px solid rgb(140, 140, 140);
        font-size: 13px;
        color: rgb(100, 100, 100);
    }

    input.login-widget-content::placeholder {
        color: rgb(140, 140, 140);
    }

    input.login-widget-content:hover {
        border: 1px solid rgb(100, 100, 100);
    }

    button.login-widget-content {
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

    input.login-widget-content.error {
        border: 1px solid rgb(227,72,67) !important;
    }
</style>