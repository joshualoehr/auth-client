<template>
    <div id="app" :class="$mq">
        <div :style="{ 'max-height': showMore ? '516px' : '466px' }" class="login-widget" :class="$mq">
            <div class="login-widget-header">
                <img :src="logo" height="70px"/>
            </div>
            <div class="login-widget-body" :class="$mq">
                <div class="login-widget-content-container">
                    <h2 class="login-widget-content">Sign in to access {{ appName }}</h2>
                    <div class="login-widget-content">{{ appDetail }}</div>
                    <Error v-if="errorMsg" :error="errorMsg" />
                    <Login v-if="activeView === 'login'"
                        :errors="errors"
                        @username-changed="errors.username = false; inputs.username = $event"
                        @password-changed="errors.password = false; inputs.password = $event"
                        @login-attempt="login()"
                    />
                    <Links 
                        :showMore="showMore"
                        @toggle-show-more="toggleShowMore()"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Error from './components/error';
import Links from './components/links';
import Login from './components/login';

export default {
    name: "app",
    components: { Error, Links, Login },
    data: () => ({
        appName: 'Test App',
        appDetail: 'Enter your AuthJL credentials to continue.',
        logo: '/logo-full.png',
        activeView: 'login',
        errorMsg: null,
        errors: {
            username: false,
            password: false
        },
        inputs: {
            username: '',
            password: ''
        },
        showMore: false,
        toggleShowMore: function() {
            this.showMore = !this.showMore;
        },
        login: function() {
            const { username, password } = this.inputs;

            if (!username) {
                this.errors.username = true;
            }
            if (!password) {
                this.errors.password = true;
            }
            if (!username || !password) {
                this.errorMsg = 'Missing one or more required fields.'
                return;
            }

            this.errorMsg = null;
            console.log(this.inputs.username, this.inputs.password);
        }
    })
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

    #app.mobile {
        padding: 0;
    }

    #app.desktop {
        padding: 6.4rem 0;
    }

    .login-widget {
        display: flex;
        flex-direction: column;
        background-color: white;
        border-radius: 3px;
        border: 1px solid rgb(221, 221, 221);
        font-family: Arial, Helvetica, sans-serif;
        overflow: hidden;
        transition: max-height 0.3s;
    }
    
    .login-widget.mobile {
        width: 100%;
        margin: auto;
    }

    .login-widget.desktop {
        margin: 0 auto;
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
        min-height: 300px;
        flex-direction: column;
        text-align: center;
    }

    .login-widget-content {
        max-height: 40px;
        flex-grow: 1;
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