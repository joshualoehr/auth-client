<template>
    <input 
        class="login-widget-content" 
        :type="password ? 'password' : 'text'" 
        :placeholder="placeholder" 
        :class="{ error: danger }"
        :value="value"
        @input="$emit('touched'); $emit('input', $event.target.value)"
        @keyup.enter="$emit('touched'); $emit('enter')"
    />
</template>

<script>
    export default {
        name: 'TextInput',
        props: {
            password: {
                type: Boolean,
                default: false
            },
            value: String,
            placeholder: String,
            touched: Boolean,
            error: Boolean
        },
        computed: {
            danger: function() {
                return this.touched && this.error;
            }
        },
        defaultModel: () => ({
            value: '',
            touched: false,
            error: false
        })
    }
</script>

<style scoped>
    .login-widget-content {
        height: 40px;
        margin: 0.4rem 0;
        border-radius: 3px;
        padding: 0 0.8rem;
        border: 1px solid rgb(140, 140, 140);
        font-size: 13px;
        color: rgb(100, 100, 100);
    }

    .login-widget-content::placeholder {
        color: rgb(140, 140, 140);
    }

    .login-widget-content:hover {
        border: 1px solid rgb(100, 100, 100);
    }

    .login-widget-content.error {
        border: 1px solid rgb(227,72,67) !important;
    }
</style>