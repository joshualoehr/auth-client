<template>
    <div id="app" :class="$mq">
        <div class="login-widget" :class="$mq">
            <div class="login-widget-header">
                <img :src="logo" height="70px"/>
            </div>
            <div class="login-widget-body" :class="$mq">
                <div class="login-widget-content-container">
                    <h2 class="login-widget-content">{{ headerText }}</h2>
                    <div v-if="subheaderText" class="login-widget-content">{{ subheaderText }}</div>
                    <Error v-if="error" :error="error" />
                    <Login v-if="activeView === 'login'" :client_id="client_id" @authenticated="handleAuthenticationSuccess" @error="error = $event"/>
                    <CreateAccount v-if="activeView === 'createAccount'" @error="error = $event"/>
                    <Consent v-if="activeView === 'consent'" 
                        :client_id="client_id" 
                        :client_name="client_name" 
                        :claims="requestedClaims" 
                        :username="authenticatedUsername" 
                        @show="activeView = $event"
                        @consentGranted="redirect"
                    />
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
const { client_id, redirect_uri, client_name, client_detail, consent_detail, logo, view } = pageData;

export default {
    name: "app",
    components: { Error, Links, Login, CreateAccount, Consent },
    data: () => ({
        client_id,
        redirect_uri,
        client_name,
        client_detail,
        consent_detail,
        logo: logo || '/logo-full.png',
        activeView: view || 'login',
        error: null,
        authenticatedUsername: null,
        requestedClaims: ['username', 'email', 'name']
    }),
    computed: {
        headerText: function() {
            return this.activeView === 'consent'
                ? `${this.client_name} will have access to:`
                : `Sign in to access ${this.client_name}`
        },
        subheaderText: function() {
            return this.activeView === 'consent' ? this.consent_detail : this.client_detail;
        }
    },
    methods: {
        handleAuthenticationSuccess: function({ username, consentGranted, id_token }) {
            this.authenticatedUsername = username;
            if (!consentGranted) {
                this.activeView = 'consent';
            } else {
                this.redirect(id_token);
            }
        },
        redirect: function(id_token) {
            window.history.pushState(this.redirect_uri);
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