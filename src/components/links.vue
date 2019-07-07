<template>
    <div class="login-widget-content">
        <div class="login-widget-links">
            <a @click="$emit('toggle-show-more')">Need help signing in?</a>
            <a href="#">Create account</a>
        </div>
        <!-- <div class="login-widget-links-more" :style="{ display: showMore ? 'flex' : 'none' }"> -->
        <div class="login-widget-links-more" :style="{ 'max-height': showMore ? '60px' : 0 }">
            <a href="#">Recover password</a>
            <a href="#">Unlock account</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "links",
        props: {
            showMore: {
                type: Boolean,
                default: () => false
            }
        }
    };
</script>

<style>
    .login-widget-content {
        height: 40px;
        flex-grow: 1;
        font-size: 16px;
    }

    .login-widget-links {
        display: flex;
        justify-content: space-between;
        margin-top: 0.8rem;
    }

    a {
        margin: auto 0;
        cursor: pointer;
        text-decoration: none;
        color: rgb(0, 125, 193)
    }

    a:hover {
        color: rgb(0, 150, 231);
    }

    .login-widget-links-more {
        display: flex;
        flex-direction: column;
        text-align: left;
        overflow: hidden;
        margin-top: 0.8rem;
    }

    .login-widget-links-more > a {
        width: 50%;
        margin-top: 0.8rem;
        transition: max-height 1.0s;
    }
</style>