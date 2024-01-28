<script>
import { RouterLink, RouterView } from 'vue-router';
// pinia 匯入的元件
// import { mapState, mapActions } from 'pinia';

export default {
    data() {
        return {
        }
    },
    components: {
        RouterLink,
        RouterView,
    },
    // pinia 匯入所需的元件
    // computed: {
    //     ...mapState(indexState, ["location", "locationInfo"])
    // },
    // methods: {
    //     ...mapActions(indexState, ["getLocation", "setLocation"]),
    // },
}
</script>

<template>
    <div class="bgArea">

        <div class="headcontent">

            <div class="layout">
                <ul class="leftMenu">
                    <li><i class="fa-solid fa-book-open-reader">
                            <RouterLink to="/" title="米花町市立圖書館"
                                style="text-decoration: none;color: black;margin-right: 10px;">
                                米花町市立圖書館</RouterLink>
                        </i></li>
                </ul>
                <ul class="rightMenu">

                    <li><a href="" title="最新消息"></a>最新消息</li>
                    <li><a href="" title="主題活動"></a>主題活動</li>
                    <li><a href="" title="數位資源"></a>數位資源</li>
                    <li>
                        <RouterLink to="/Booking" title="我要借書" style="text-decoration: none;color: black;">我要借書
                        </RouterLink>
                    </li>

                </ul>
            </div>

        </div>

    </div>
</template>

<style lang="scss" scoped>
.bgArea {
    width: 100vw;
}

.headcontent {
    width: 100vw;
    height: 13vh;
    display: flex;
    flex-direction: column;

    .layout {
        display: flex;
        height: 13vh;
        background-color: #ececec;

        .leftMenu,
        .rightMenu {
            width: 50vw;
            height: 13vh;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            list-style-type: none;
            font-size: 14pt;
        }

        .leftMenu li,
        .rightMenu li {
            margin-right: 20px; // 調整選項間的間距
            position: relative;
        }

        .leftMenu li::before,
        .rightMenu li::before {
            content: "|"; // 分隔線
            position: absolute;
            left: -12px; // 調整分隔線位置
        }

        .leftMenu li:first-child::before,
        .rightMenu li:first-child::before {
            content: ""; // 第一個選項前面不需要分隔線
        }

        .fa-solid {
            margin-right: 5px;
        }
    }

    .d-flex {
        width: 15vw;
    }

}
</style>
