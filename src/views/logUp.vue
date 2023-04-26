<template>
    <div id="poster">
    
        <el-form :model="ruleForm" ref="ruleForm" label-width="0px" leble-position="left" class="demo-ruleForm">
    
            <h3 class="register-container">
    
                系统登陆
    
                <el-button @click="toLogin()">去登陆</el-button>
    
            </h3>
    
            <el-form-item label="" prop="login Name">
    
                <el-input type="text" v-model="ruleForm.LoginName" placeholder="请输入用户名"></el-input>
    
            </el-form-item>
    
            <el-form-item label="" prop="name">
    
                <el-input v-model="ruleForm.age" placeholder="请输入网名"></el-input>
    
            </el-form-item>
    
    
    
            <el-form-item label="" prop="pass">
    
                <el-input type="password" v-model="ruleForm.pass" autocomplete="off" placeholder="请输入密码"></el-input>
    
            </el-form-item>
    
            <el-form-item label="确认密码" prop="checkPass">
    
                <el-input type="password" v-model="ruleForm.checkPass" placeholder="请输入确认密码" autocomplete="off"></el-input>
    
            </el-form-item>
    
            <el-form-item label="年龄" prop="age">
    
                <el-input v-model.number="ruleForm.age"></el-input>
    
            </el-form-item>
    
            <el-form-item>
    
                <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
    
                <el-button @click="resetForm('ruleForm')">重置</el-button>
    
            </el-form-item>
    
        </el-form>
    
    </div>
</template>
  
<script>
export default {
    name: 'Home',
    data() {
        var checkAge = (rule, value, callback) => {
            if (!value) {
                return callback(new Error('年龄不能为空'));
            }
            setTimeout(() => {
                if (!Number.isInteger(value)) {
                    callback(new Error('请输入数字值'));
                } else {
                    if (value < 18) {
                        callback(new Error('必须年满18岁'));
                    } else {
                        callback();
                    }
                }
            }, 1000);
        };
        var validatePass = (rule, value, callback) => {
            if (value === '') {
                callback(new Error('请输入密码'));
            } else {
                if (this.ruleForm.checkPass !== '') {
                    this.$refs.ruleForm.validateField('checkPass');
                }
                callback();
            }
        };
        var validatePass2 = (rule, value, callback) => {
            if (value === '') {
                callback(new Error('请再次输入密码'));
            } else if (value !== this.ruleForm.pass) {
                callback(new Error('两次输入密码不一致!'));
            } else {
                callback();
            }
        };
        return {
            ruleForm: {
                pass: '',
                checkPass: '',
                age: ''
            },
            rules: {
                pass: [
                    { validator: validatePass, trigger: 'blur' }
                ],
                checkPass: [
                    { validator: validatePass2, trigger: 'blur' }
                ],
                age: [
                    { validator: checkAge, trigger: 'blur' }
                ]
            }
        };
    },
    methods: {
        submitForm(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    alert('submit!');
                } else {
                    console.log('error submit!!');
                    return false;
                }
            });
        },
        resetForm(formName) {
            this.$refs[formName].resetFields();
        }
    }



};
</script>
  
<style>
#poster {
    background-position: center;
    height: 100%;
    width: 100%;
    background-size: cover;
    position: fixed;
}

body {
    margin: 0px;
    padding: 0px;
}

.register-container {
    border-radius: 15px;
    background-clip: padding-box;
    margin: 90px auto;
    width: 350px;
    padding: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
}

.register-title {
    margin: 0px auto 40px auto;
    text-align: center;
    color: #505458;
}
</style>