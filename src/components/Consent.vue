<template>
    <div id="login-widget-consent-container">
        <ul>
            <li v-for="([claim, claimText]) in claimsText" :key="claim">
                {{ claimText }}
            </li>
        </ul>
        <div class="login-widget-allow-text">Allow {{ client_name }} to do this?</div>
        <button @click="sendConsent">Allow</button>
        <a @click="$emit('show', 'login')">Cancel</a>
    </div>
</template>

<script>
    export default {
        name: 'Consent',
        props: {
            client_id: String,
            client_name: String,
            username: String,
            claims: Array
        },
        data: () => ({
            claimsMap: {
                'username': 'Username',
                'email': 'Email',
                'name': 'First and last name'
            }
        }),
        computed: {
            claimsText: function() {
                return this.claims.map(claim => ([claim, this.claimsMap[claim]]));
            }
        },
        methods: {
            sendConsent: function() {
                const { username, client_id } = this;
                fetch('/consent', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ username, client_id })
                })
                .then(({ id_token }) => {
                    this.$emit('consentGranted', id_token);
                })
                .catch(console.error);
            }
        }
    }
</script>

<style scoped>
    #login-widget-consent-container {
        flex-grow: 3;
        min-width: 240px;
        width: 100%;
        display: flex;
        flex-direction: column;
    }

    ul {
        list-style-type: square;
        text-align: left;
        margin-top: 0;
        margin-bottom: 1.0rem;
    }

    li {
        margin-bottom: 0.4rem;
    }

    div {
        color: rgb(100, 100, 100);
    }

    .login-widget-allow-text {
        text-align: center;
        margin-bottom: 0.8rem;
    }

    button {
        height: 40px;
        border-radius: 3px;
        margin: 0.8rem 0;
        cursor: pointer;
        color: white;
        background-image: linear-gradient(rgb(0, 134, 194), rgb(0, 118, 171));
        border: 1px solid rgb(0, 69, 106);
        padding: 0.4rem 0;
        font-size: 14px;
    }

    button:hover {
        background-image: linear-gradient(rgb(0, 154, 222), rgb(0, 134, 194));
    }

    a {
        margin: 0 auto;
        font-size: 13px;
        cursor: pointer;
        text-decoration: none;
        color: rgb(0, 125, 193)
    }

    a:hover {
        color: rgb(0, 150, 231);
    }
</style>