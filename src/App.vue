<template>
    <div id="app">
        <el-form :inline="true">
            <el-form-item>
                <el-image src="http://localhost/kaptcha/img" onclick="this.src='http://localhost/kaptcha/img?d='+new Date()*1"></el-image>
            </el-form-item>
            <el-form-item>
                <el-input v-model="code" style="width: 150px"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button @click="checkCode" type="primary">Check</el-button>
            </el-form-item>
        </el-form>


    </div>
</template>

<script>
    export default {
        data() {
            return {
                code: ""
            }
        },
        methods: {
            async checkCode() {
                const {
                    data: res
                } = await this.$http.get(`http://localhost/kaptcha/check/${this.code}`);
                if (res.code === 200) {
                    this.$notify({
                        title: 'It works!',
                        type: 'success',
                        message: '验证码校验正确',
                        duration: 2000
                    })
                } else {
                    this.$notify({
                        title: 'It do not works!',
                        type: 'error',
                        message: '校验失败',
                        duration: 2000
                    })
                }
            }
        }
    }
</script>

<style>
    #app {
        font-family: Helvetica, sans-serif;
        text-align: center;
    }
</style>
