<template>
    <section>
        <h2 id="weekly">Weekly Forecast</h2>
        <div class="items">
            <div class="day" v-for="(data, index) in dailyWeather" :key="index">
                <h2>{{ generateDay(data.dt) }}</h2>
                <p>{{ generateDate(data.dt) }}</p>
                <h3>{{ Math.ceil(data.feels_like.day) }}&#176;</h3>
                <p>{{ data.weather[0].description }}</p>
                <img :src="generateIcon(data.weather[0].icon)">
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        name: 'WeeklyForecast',
        props: ['dailyWeather'],
        methods: {
            generateIcon(ico) {
                return `http://openweathermap.org/img/wn/${ico}@2x.png`
            },
            generateDay(dt) {
                const days = [
                    'Sunday',
                    'Monday',
                    'Tuesday',
                    'Wednesday',
                    'Thursday',
                    'Friday',
                    'Saturday'
                ]
                let date = new Date(dt * 1000)
                let day = date.getDay()
                return days[day]
            },
            generateDate(dt) {
                let dateTime = new Date(dt * 1000)
                let dateStr = dateTime.toDateString().split(' ')
                dateStr.splice(0, 1)
                dateStr.splice(dateStr.length - 1)
                return dateStr.join(' ')
            }
        }
    }
</script>

<style>
    section {
        width: 100vw;
    }
    .items {
        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }
    .day {
        margin: 2px;
        background-color: lightgray;
        width: 200px;
        border: 2px solid gray;
        border-radius: 15px;
        margin: 20px;
    }
    #weekly {
        font-family: sans-serif, cursive;
        color: darkgray;
        font-size: 25px;
    }
</style>