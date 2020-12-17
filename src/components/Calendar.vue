<template>
    <div class="calendar">
        <span
            class="switch switch__prev"
            @click="switchDate('prev')"
        >上一个</span>
        <div class="main">
            <span>{{ date.toLocaleString() }}</span>
            <div class="weeks">
                <div
                    v-for="(day, index) in 7"
                    :key="day"
                    class="weeks__day"
                >
                    {{ weekDescs[index] }}
                </div>
            </div>
            <div class="days">
                <div
                    v-for="day in days"
                    :key="day"
                    class="day"
                    :class="{
                        'day--today': day === today,
                        'day--unsignin': !dayIsSigin(day) && day < today,
                        'day--signin': dayIsSigin(day)
                    }"
                >
                    {{ day }}
                </div>
            </div>
        </div>
        <span
            class="switch switch__next"
            @click="switchDate('next')"
        >下一个</span>
    </div>
</template>

<script>
    export default {
        components: {},
        props: {
            // 当前日历日期
            date: {
                type: [ String, Date ],
                default: ''
            },
            // 一周对应描述
            weekDescs: {
                type: Array,
                default: () => ([ '一', '二', '三', '四', '五', '六', '日' ])
            },
            // 签到天数
            list: {
                type: Array,
                default: () => ([ 1, 2 ])
            }
        },
        data () {
            return {
                // 设置月份
                month: -1,
                // 设置年份
                year: -1,
                // 月份天数
                days: 0
            }
        },
        computed: {
            today () {
                return new Date().getDate()
            }
        },
        watch: {
            date: {
                immediate: true,
                handler (newVal) {
                    this.parseDate(newVal)
                }
            }
        },
        created () {
        },
        mounted () { },
        methods: {
            parseDate () {
                const { date } = this

                let parseDate

                if (date instanceof Date) {
                    parseDate = date
                } else {
                    parseDate = new Date(date)
                }

                const month = parseDate.getMonth()
                const year = parseDate.getFullYear()

                const tempDate = new Date(year, month + 1, 0)

                const days = tempDate.getDate()

                this.month = month
                this.year = year
                this.days = days
            },
            dayIsSigin (day) {
                return this.list.includes(day)
            },
            // 日期切换
            switchDate (type) {
                const { year = 0, month = 0 } = this

                if (month == -1 || year === -1) return
                const setMouth = type === 'next' ? month + 1 : month - 1
                const date = new Date(year, setMouth, 1)

                this.$emit('switchDate', date)
            }
        }
    }
</script>

<style scoped>
    .calendar {
        display: flex;
        justify-content: center;
    }

    .main {
        width: 630rpx;
    }

    .weeks {
        display: flex;
    }
    .weeks__day {
        display: flex;
        justify-content: center;
        align-items: center;

        width: 90rpx;
        height: 90rpx;
    }
    .days {
        display: flex;
        flex-wrap: wrap;
    }
    .day {
        display: flex;
        justify-content: center;
        align-items: center;

        /* border: 1rpx solid #e1e1e1; */
        width: 90rpx;
        height: 90rpx;
    }

    .day--today {
        color: red;
    }

    .day--unsignin {
        background-color: #ccc;
    }

    .day--signin {
        background-color: #fff;
    }

    .switch {
        display: inline-flex;
        align-items: center;

        width: 60rpx;

        text-align: center;
    }
</style>