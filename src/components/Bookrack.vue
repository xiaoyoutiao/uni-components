<template>
<view class='bookrack'>
    <text class="title">为你推荐</text>
    <text class="desc">基于你的阅读历史计算·每日更新</text>
    <view class="main">
        <view :class="['book', isStartAnimate && 'book--animate']" v-for="(chunk, index) in list" :key="index" :style="`animation-delay: ${index * delay}s`">
            <view 
                :class="['book__item', chunkIndex === 0 && 'book__item--reveser', chunkIndex === 0 && isStartAnimate && 'book__item--animate']"
                v-for="(book, chunkIndex) in chunk" :key="chunkIndex"
                :style="`animation-delay: ${index  * delay}s`"
                >{{ book }}</view>
        </view>
    </view>
    <view class="switch-btn" @click="change">换一批</view>
</view>
</template>

<script>
    import lodashChunk from '@/utils/chunk'

    export default {
        components: {},
        props: {},
        data () {
            return {
                delay: 0.5,
                list: [],
                isStartAnimate: false
            }
        },
        computed: {
        },
        watch: {
            isStartAnimate (newVal) {
                console.log(newVal);
            }
        },
        created () {
            this.change()
        },
        mounted () {
        },
        methods: {
            async startAnimate () {
                this.isStartAnimate = false
                await this.$nextTick()
                this.isStartAnimate = true
            },
            async change () {
                this.list = lodashChunk([ 1, 2, 1, 2, 1, 2, 1, 2, 1, 2 ], 2)
                await this.$nextTick()
                this.startAnimate()
            }
        }
    }
</script>

<style scoped>
    .bookrack {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;

        border-radius: 15rpx;

        width: 690rpx;
        padding: 45rpx 0;

        background-color: #fff;
    }

    .title {
        font-size: 46rpx;
        font-weight: 700;

        color: #2c3e50;
    }

    .desc {
        color: #c5c5c5;
        font-size: 32rpx;
        line-height: 65rpx;
    }

    .switch-btn {
        margin-top: auto;
        width: 80%;
        height: 95rpx;

        border-radius: 10rpx;

        font-size: 32rpx;
        font-weight: 700;
        line-height: 95rpx;
        text-align: center;

        background-color: #f7f7f9;
        color: #007af3;
    }

    .main {
        display: flex;
        flex-wrap: wrap;

        width: 100%;
        margin: 50rpx 0;

        background-color: #fff;
    }

    .book {
        counter-reset: section 1;
        counter-increment: section 0.1;
        position: relative;

        width: 210rpx;
        margin: 10rpx;
        height: 280rpx;
    }
    .book--animate {
        animation: rotate 0.5s linear 1;
        animation-fill-mode: forwards;
    }

    .book__item {
        position: absolute;
        top: 0;
        left: 0;
        font-size: 80rpx;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100%;
        background-color: rgba(137, 224, 163, 0.74);
    }

    .book__item--reveser {
        background-color: rgba(196, 130, 110, 0.603);
    }
    .book__item--animate {
        animation: rotateReveser 0.5s linear 1;
        animation-fill-mode: forwards;
    }

    @keyframes rotate {
        form {
            transform: rotateY(0);
        }
        to {
            transform: rotateY(180deg);
        }
    }
    @keyframes rotateReveser {
        form {
            /* transform: rotateY(180deg); */
        }
        to {
            z-index: 2;
            /* transform: rotateY(360deg); */
        }
    }
</style>