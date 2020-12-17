<template>
    <view class="main">
        <Calendar
            :date="date"
            @switchDate="onSwitchDate"
        />
    </view>
</template>

<script>
    import Bookrack from '@/components/Bookrack'
    import Calendar from '@/components/Calendar'

    export default {
        components: {
            Bookrack,
            Calendar
        },
        data () {
            return {
                date: new Date()
            }
        },
        computed: {},
        watch: {},
        onLoad () { },
        onShow () { },
        methods: {
            onSwitchDate (date) {
                this.date = date
            }
        }
    }
</script>

<style>
    page {
        background-color: #f1f1f1;
    }
</style>

<style scoped>
    .main {
        display: flex;
        justify-content: center;

        width: 750rpx;
        padding-top: 30rpx;
    }
</style>