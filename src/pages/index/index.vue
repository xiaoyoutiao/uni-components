<template>
<view class='main'>
	<Bookrack></Bookrack>
</view>
</template>

<script>
    import Bookrack from '@/components/Bookrack'

    export default {
        components: {
            Bookrack
        },
        data () {
            return {}
        },
        computed: {},
        watch: {},
        onLoad () { },
        onShow () { },
        methods: {}
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
    }
</style>