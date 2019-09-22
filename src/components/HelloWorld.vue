<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <button @click="createOrder">京东支付</button>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        methods: {
            createOrder() {
                axios.interceptors.request.use(
                    config => {
                        config.headers['Authorization'] = 'Bearer eyJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1Njk3OTUwMTEsInN1YiI6ImFkbWluc2hpdHUiLCJjcmVhdGVkIjoxNTY5MTkwMjExMTU4fQ.FvvylJq35KL6Z5XxOAu0_KAF9iHoagZvcbekxiMRSiWYFdcL3-jxLQeqLdVLS0lzM-_CznEJw7NoZ-A4sWdFLA'
                        return config
                    }
                )
                axios
                    .post('http://127.0.0.1:8080/paper/createOrder',
                    )
                    .then(response => (this.info = response))
                    .catch(function (error) { // 请求失败处理
                        console.log(error);
                    });
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
