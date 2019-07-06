<template>
    <div id="app" :class="$mq">
        <div class="login-widget" :class="$mq">
            <div class="login-widget-header">
                <img v-bind:src="logo" height="70px"/>
            </div>
            <div class="login-widget-body" :class="$mq">
                <form>
                    <div class="login-widget-form-content">
                        <h2 class="login-widget-content">Sign in to access {{ appName }}</h2>
                        <div class="login-widget-content">{{ appDetail }}</div>
                        <input class="login-widget-content" type="text" placeholder="Email or Username"/>
                        <input class="login-widget-content" type="text" placeholder="Password"/>
                        <input class="login-widget-content" type="submit" value="Sign in"/>
                        <div class="login-widget-links login-widget-content">
                            <a href="#">Need help signing in?</a>
                            <a href="#">Create account</a>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "app",
    data: () => ({
        appName: 'Test App',
        appDetail: 'Enter your AuthJL credentials to continue.',
        logo: '/logo-full.png'
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
    }
    
    .login-widget.mobile {
        width: 100%;
        margin: auto;
    }

    .login-widget.desktop {
        height: 466px;
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
        padding: 1.4rem 2.8rem;
        flex-grow: 1;
    }

    .login-widget-body > form {
        display: flex;
        flex-direction: column;
        height: 100%;
        text-align: center;
    }

    .login-widget-form-content {
        display: flex;
        margin: auto;
        max-width: 466px;
        min-height: 310px;
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

    input.login-widget-content {
        margin: 0.4rem 0;
        border-radius: 3px;
    }

    input[type=text].login-widget-content {
        padding: 0 0.8rem;
        border: 1px solid rgb(140, 140, 140);
        font-size: 13px;
    }

    input[type=text].login-widget-content::placeholder {
        color: rgb(140, 140, 140);
    }

    input[type=submit].login-widget-content {
        margin: 0.8rem 0;
        cursor: pointer;
        color: white;
        background-image: linear-gradient(rgb(0, 134, 194), rgb(0, 118, 171));
        border: 1px solid rgb(0, 69, 106);
        padding: 0.4rem 0;
        font-size: 14px;
    }

    input[type=submit].login-widget-content:hover {
        background-image: linear-gradient(rgb(0, 154, 222), rgb(0, 134, 194));
    }

    .login-widget-links {
        display: flex;
        justify-content: space-between;
        margin-top: 0.8rem;
    }

    .login-widget-links > a {
        margin: auto 0;
        cursor: pointer;
        text-decoration: none;
        color: rgb(0, 125, 193)
    }

    .login-widget-links > a:hover {
        color: rgb(0, 150, 231);
    }
</style>