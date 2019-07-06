<template>
    <div class="login-widget-content login-widget-errors-container" v-if="error">
        <div class="login-widget-error">
            <div style="display: flex; width: 40px; height: 40px; border-right: 1px solid rgb(221, 221, 221)">
                <img style="display: block; margin: auto;" src="/alert.svg" height="25px"/>
            </div>
            <span style="padding-left: 0.8rem;">{{ error }}</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'error',
        props: ['error']
    }
</script>

<style scoped>
    .login-widget-content {
        max-height: 40px;
        flex-grow: 1;
        font-size: 16px;
    }

    .login-widget-errors-container {
        display: flex;
        flex-direction: column;
        text-align: left;
        margin-bottom: 0.8rem;
    }
    
    .login-widget-error {
        display: flex;
        font-size: 13px;
        margin-bottom: 0.4rem;
        border: 1px solid rgb(221, 221, 221);
        border-radius: 3px;
        height: 40px;
        line-height: 40px;
    }
</style>