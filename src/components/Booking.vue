<script>
import Header from '../components/Header.vue';
import Swal from 'sweetalert2'

export default {
    data() {
        return {
            // 註冊帳戶
            user: {
                username: "",
                phoneNumber: "",
                password: "",
            },
            // 數字驗證
            userInput: "",
            captchaValue: ""
        };
    },
    mounted() {
        const signInBtn = document.getElementById("signIn");
        const signUpBtn = document.getElementById("signUp");
        const firstForm = document.getElementById("form1");
        const secondForm = document.getElementById("form2");
        const container = document.querySelector(".container");

        signInBtn.addEventListener("click", this.handleSignInClick);
        signUpBtn.addEventListener("click", this.handleSignUpClick);
        firstForm.addEventListener("submit", this.handleFirstFormSubmit);
        secondForm.addEventListener("submit", this.handleSecondFormSubmit);

        // 數字驗證
        // this.generateCaptcha();
    },
    methods: {
        handleSignInClick() {
            this.containerClassRemove("right-panel-active");
        },
        handleSignUpClick() {
            this.containerClassAdd("right-panel-active");
        },
        handleFirstFormSubmit(e) {
            e.preventDefault();
        },
        handleSecondFormSubmit(e) {
            e.preventDefault();
        },
        containerClassRemove(className) {
            const container = document.querySelector(".container");
            if (container) {
                container.classList.remove(className);
            }
        },
        containerClassAdd(className) {
            const container = document.querySelector(".container");
            if (container) {
                container.classList.add(className);
            }
        },
        // 註冊
        async registerUser() {
            try {
                const response = await fetch("http://localhost:8080/api/library/registerUser", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify(this.user),
                });

                if (!response.ok) {
                    await Swal.fire({
                        icon: 'error',
                        title: '註冊失敗',
                        text: '註冊出現問題！',
                    });
                    return;
                }

                const data = await response.json();

                await Swal.fire({
                    icon: 'success',
                    title: '註冊成功',
                    text: '您已成功註冊！',
                });

                console.log("Registration successful", data);
            } catch (error) {
                await Swal.fire({
                    icon: 'error',
                    title: '錯誤',
                    text: `取得資料時發生錯誤: ${error.message}`,
                });
            }
        }

        // 數字驗證
        // generateRandomNumber() {
        //     return Math.floor(Math.random() * 10);
        // },
        // generateCaptcha() {
        //     const canvas = this.$refs.captchaCanvas;
        //     const ctx = canvas.getContext('2d');

        //     ctx.clearRect(0, 0, canvas.width, canvas.height);

        //     this.captchaValue = this.generateRandomNumber();

        //     ctx.font = '30px Arial';
        //     ctx.fillText(this.captchaValue, 80, 60);
        // },
        // checkCaptcha() {
        //     if (this.userInput === this.captchaValue.toString()) {
        //         // 使用 SweetAlert2 來替代 alert
        //         Swal.fire({
        //             icon: 'success',
        //             title: '驗證成功！',
        //         });
        //     } else {
        //         // 使用 SweetAlert2 來替代 alert
        //         Swal.fire({
        //             icon: 'error',
        //             title: '驗證失敗，請重新輸入。',
        //         });

        //         this.generateCaptcha();
        //     }
        // }
    }
}
</script>

<template>
    <div class="container right-panel-active" style="margin-top: 10vh;">
        <!-- 註冊 -->
        <div class="container__form container--signup">
            <form @submit.prevent="registerUser" class="form" id="form1">
                <h2 class="form__title">建立帳戶</h2>
                <input v-model="user.username" type="text" placeholder="使用者名稱" class="input" />
                <input v-model="user.phoneNumber" type="text" placeholder="手機號碼" class="input" />
                <input v-model="user.password" type="password" placeholder="密碼" class="input" />
                <button type="submit" class="btn">註冊</button>
            </form>
        </div>

        <!-- 登入 -->
        <div class="container__form container--signin">
            <form action="#" class="form" id="form2">
                <h2 class="form__title">登入</h2>
                <input type="text" placeholder="手機號碼" class="input" />
                <input type="password" placeholder="密碼" class="input" />

                <!-- <div id="captcha_container" style="border: 1px solid blue; height: 100px;">
                    <h6>驗證碼：</h6>
                    <canvas ref="captchaCanvas" width="100" height="80"></canvas>
                    <input type="text" v-model="userInput" placeholder="輸入數字">
                    <button @click="checkCaptcha">驗證</button>
                </div> -->

                <a href="#" class="link">忘記密碼?</a>
                <button class="btn">登入</button>
            </form>
        </div>

        <!-- 頁面切換 -->
        <div class="container__overlay">
            <div class="overlay">
                <div class="overlay__panel overlay--left">
                    <button class="btn" id="signIn">已有帳號</button>
                </div>
                <div class="overlay__panel overlay--right">
                    <button class="btn" id="signUp">沒有帳號</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
:root {
    --white: #e9e9e9;
    --gray: #333;
    --blue: #0367a6;
    --lightblue: #008997;

    --button-radius: 0.7rem;

    --max-width: 758px;
    --max-height: 420px;
}

// 框架
.container {
    background-color: var(--white);
    border-radius: var(--button-radius);
    box-shadow: 0 0.9rem 1.7rem rgba(0, 0, 0, 0.25),
        0 0.7rem 0.7rem rgba(0, 0, 0, 0.22);
    height: var(--max-height);
    max-width: var(--max-width);
    overflow: hidden;
    position: relative;
    width: 100%;
}

// 註冊、登入 框框
.container__form {
    height: 100%;
    position: absolute;
    top: 0;
    transition: all 0.6s ease-in-out;
}

.container--signin {
    left: 0;
    width: 50%;
    z-index: 2;
}

.container.right-panel-active .container--signin {
    transform: translateX(100%);
}

.container--signup {
    left: 0;
    opacity: 0;
    width: 50%;
    z-index: 1;
}

.container.right-panel-active .container--signup {
    animation: show 0.6s;
    opacity: 1;
    transform: translateX(100%);
    z-index: 5;
}

// 頁面切換
.container__overlay {
    height: 100%;
    left: 50%;
    overflow: hidden;
    position: absolute;
    top: 0;
    transition: transform 0.6s ease-in-out;
    width: 50%;
    z-index: 100;
}

.container.right-panel-active .container__overlay {
    transform: translateX(-100%);
}

.overlay {
    background-color: var(--lightblue);
    background-image: url("../../picture/玉山銀行.png");
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    height: 100%;
    left: -100%;
    position: relative;
    transform: translateX(0);
    transition: transform 0.6s ease-in-out;
    width: 200%;
}

.container.right-panel-active .overlay {
    transform: translateX(50%);
}

.overlay__panel {
    align-items: center;
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: center;
    position: absolute;
    text-align: center;
    top: 0;
    transform: translateX(0);
    transition: transform 0.6s ease-in-out;
    width: 50%;
}

.overlay--left {
    transform: translateX(-20%);
}

.container.right-panel-active .overlay--left {
    transform: translateX(0);
}

.overlay--right {
    right: 0;
    transform: translateX(0);
}

.container.right-panel-active .overlay--right {
    transform: translateX(20%);
}

// 按鈕
.btn {
    background-color: var(--blue);
    background-image: linear-gradient(90deg, var(--blue) 0%, var(--lightblue) 74%);
    border-radius: 20px;
    border: 1px solid var(--blue);
    color: var(--white);
    cursor: pointer;
    font-size: 0.8rem;
    font-weight: bold;
    letter-spacing: 0.1rem;
    padding: 0.9rem 4rem;
    text-transform: uppercase;
    transition: transform 80ms ease-in;
}

.form>.btn {
    margin-top: 1.5rem;
}

.btn:active {
    transform: scale(0.95);
}

.btn:focus {
    outline: none;
}

// 表單
.form {
    background-color: var(--white);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 0 3rem;
    height: 100%;
    text-align: center;
}

.input {
    background-color: #fff;
    border: none;
    padding: 0.9rem 0.9rem;
    margin: 0.5rem 0;
    width: 100%;
}
</style>