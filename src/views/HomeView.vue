<script>
import Header from '../components/Header.vue';

export default {
    data() {
        return {

        }
    },
    components: {
        Header,
    }
}
</script>

<template>
    <div class="bgARea">

        <div class="newsArea">
            <div class="title">
                <h2>精選電子書</h2>
            </div>

            <div class="cardArea">

                <div class="card" style="width: 18rem;">
                    <img src="../../picture/打造你要的人生.png" class="card-img-top" alt="打造你要的人生">
                    <div class="card-body">
                        <h5 class="card-title">打造你要的人生</h5>
                        <p class="card-text">有意義的工作是打造快樂生活的支柱。你的快樂應該只與自己有關，學習提高自我管理的效能，從工作中找到自我認同，聚焦於他人的快樂而非自己的幸福。
                        </p>
                        <a href="#" class="btn btn-primary">更多資訊</a>
                    </div>
                </div>

                <div class="card" style="width: 18rem;">
                    <img src="../../picture/逆思維.png" class="card-img-top" alt="逆思維">
                    <div class="card-body">
                        <h5 class="card-title">逆思維</h5>
                        <p class="card-text">在飛快改變的世界，學會「質疑」才能不被淘汰。「想法轉個彎，人生路更寬！」。翻轉危局的解答並不一定在前方，而在你的每一個「想不到」裡。
                        </p>
                        <a href="#" class="btn btn-primary">更多資訊</a>
                    </div>
                </div>

                <div class="card" style="width: 18rem;">
                    <img src="../../picture/成人世界生存邏輯.png" class="card-img-top" alt="成人世界生存邏輯">
                    <div class="card-body">
                        <h5 class="card-title">成人世界生存邏輯</h5>
                        <p class="card-text">成人世界生存邏輯沒別的，就是面對失敗、驗證失敗、挑戰失敗，每當我們失敗的次數越多，避免失敗的能力就越強,，透過反思，跳脫自己人生的預設道路。
                        </p>
                        <a href="#" class="btn btn-primary">更多資訊</a>
                    </div>
                </div>

            </div>
        </div>

        <div class="footerArea">
            <h6>Kai 版權所有 © 2024 All Rights Reserved.</h6>
        </div>

    </div>
</template>

<style lang="scss">
.bgArea {
    width: 100vw;
}

.newsArea {
    width: 80vw;
    height: 90vh;
    margin-left: 10vw;
    margin-top: 5vh;
    // border: 1px solid blue;

    .title {
        position: relative;
        width: 200px;
        margin-top: 5vh;

        h2 {
            margin-left: 30px;
        }

        ::after {
            content: "";
            width: 100%;
            height: 10px;
            background: #db9d3a;
            position: absolute;
            left: 10px;
            top: 100%;
        }
    }

    .cardArea {
        display: flex;
        justify-content: space-around;
        margin-top: 5vh;
    }
}

.footerArea {
    width: 100vw;
    height: 10vh;
    background-color: #ececec;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
}
</style>
