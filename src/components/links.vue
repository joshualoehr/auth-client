<template>
    <div id="login-widget-links-container">
        <div v-if="activeView === 'login'">
            <div class="login-widget-links" style="justify-content: space-between;">
                <a class="login-widget-link" @click="showMore = !showMore">Need help signing in?</a>
                <a class="login-widget-link" @click="showMore = false; $emit('show', 'createAccount')">Create account</a>
            </div>
            <div class="login-widget-links-more" :style="{ 'max-height': showMore ? '80px' : 0 }">
                <a class="login-widget-link">Recover password</a>
                <a class="login-widget-link">Unlock account</a>
            </div>
        </div>
        <div v-if="activeView === 'createAccount'">
            <div class="login-widget-links" style="justify-content: center;">
                <a class="login-widget-link" @click="$emit('show', 'login')">Back to sign in</a>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "links",
        props: {
            activeView: String
        },
        data: () => ({
            showMore: false
        })
    };
</script>

<style scoped>
    #login-widget-links-container {
        flex-grow: 1;
        font-size: 16px;
    }

    .login-widget-links {
        display: flex;
        /* justify-content: space-between; */
        margin-top: 0.8rem;
    }

    a.login-widget-link {
        margin: auto 0;
        cursor: pointer;
        text-decoration: none;
        color: rgb(0, 125, 193)
    }

    a.login-widget-link:hover {
        color: rgb(0, 150, 231);
    }

    .login-widget-links-more {
        display: flex;
        flex-direction: column;
        text-align: left;
        overflow: hidden;
        margin-top: 0.8rem;
        transition: max-height 0.15s linear;
    }

    .login-widget-links-more > a.login-widget-link {
        width: 50%;
        margin-top: 0.8rem;
    }
</style>