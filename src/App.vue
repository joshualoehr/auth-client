<template>
    <div id="app" :class="$mq">
        <div class="login-widget" :class="$mq">
            <div class="login-widget-header">
                <img :src="logo" height="70px"/>
            </div>
            <div class="login-widget-body" :class="$mq">
                <div class="login-widget-content-container">
                    <h2 class="login-widget-content">{{ headerText }}</h2>
                    <div v-if="activeView !== 'consent'" class="login-widget-content">{{ activeView === 'consent' ? consentDetail : appDetail }}</div>
                    <Error v-if="error" :error="error" />
                    <Login v-if="activeView === 'login'" @error="error = $event"/>
                    <CreateAccount v-if="activeView === 'createAccount'" @error="error = $event"/>
                    <Consent v-if="activeView === 'consent'" :appName="appName" :claims="requestedClaims" @show="activeView = $event"/>
                    <Links v-if="activeView !== 'consent'" :activeView="activeView" @show="activeView = $event"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Error from './components/error';
import Links from './components/links';
import Login from './components/login';
import CreateAccount from './components/CreateAccount';
import Consent from './components/Consent';

const pageData = JSON.parse(document.getElementById('pageData').innerHTML);

export default {
    name: "app",
    components: { Error, Links, Login, CreateAccount, Consent },
    data: () => ({
        ...pageData,
        logo: '/logo-full.png',
        activeView: 'login',
        error: null,
    }),
    computed: {
        headerText: function() {
            return this.activeView === 'consent'
                ? `${this.appName} will have access to:`
                : `Sign in to access ${this.appName}`
        }
    }
}
</script>

<style scoped>
    #app {
        display: flex;
        position: absolute;
        left: 0;
        top: 0;
        width: 100vw;
        height: 100vh;
        background-color: rgb(250, 250, 250);
    }

    .login-widget {
        display: flex;
        flex-direction: column;
        background-color: white;
        border-radius: 3px;
        border: 1px solid rgb(221, 221, 221);
        font-family: Arial, Helvetica, sans-serif;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: auto;
    }
    
    .login-widget.mobile {
        margin-top: auto;
        width: 100%;
    }

    .login-widget.desktop {
        margin-top: 20vh;
        width: 400px;
    }

    .login-widget-header {
        display: flex;
        flex-shrink: 1;
        border-bottom: 1px solid rgb(221, 221, 221);
        height: 90px;
    }

    .login-widget-header > img {
        display: block; 
        margin: auto;
    }

    .login-widget-body {
        display: flex;
        flex-direction: column;
        text-align: center;
        padding: 1.4rem 2.8rem;
    }

    .login-widget-content-container {
        display: flex;
        margin: auto;
        max-width: 466px;
        flex-direction: column;
        text-align: center;
        overflow: hidden;
    }

    .login-widget-content {
        height: 40px;
        font-size: 16px;
    }

    h2.login-widget-content {
        margin: 0;
        color: rgb(94, 94, 94);
    }

    div.login-widget-content {
        color: rgb(119, 119, 119);
    }
</style>