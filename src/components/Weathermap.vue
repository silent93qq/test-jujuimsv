<template>
    <div>
        <h1 class="text-center m-5">Test</h1>

        <ul class="nav nav-tabs nav-justified">
            <div v-for="item in city" :key="item">
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="setActive(item.value,item.key)"
                       :class="{ active: isActive(item.value) }"
                       :href=item.key>{{item.value}}</a>
                </li>
            </div>
        </ul>

        <div class="tab-content py-3" id="myTabContent">
            <div class="tab-pane fade" :class="{ 'active show': isActive(activeItem) }" :id=activeItem>
                <table class="table">
                    <thead>
                    <tr>
                        <th scope="col">City</th>
                        <th scope="col">Temperature</th>
                        <th scope="col">Atmospheric pressure</th>
                        <th scope="col">Humidity</th>
                        <th scope="col">Wind speed</th>
                        <th scope="col">Wind direction</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr>
                        <td>{{activeItem}}</td>
                        <td>{{info.data.main.temp}} °C</td>
                        <td>{{info.data.main.pressure}} hPa</td>
                        <td>{{info.data.main.humidity}} %</td>
                        <td>{{info.data.wind.speed}} meter/sec</td>
                        <td>{{info.data.wind.deg}} °</td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

</template>

<script>
    import Vue from 'vue'
    import axios from 'axios'
    import VueAxios from 'vue-axios'

    Vue.use(VueAxios, axios)
    export default {
        name: "Weathermap",
        data() {
            return {
                info: null,
                url: 'https://api.openweathermap.org/data/2.5/weather',
                id: 'c2dcf8ffb5cdc3f8977bfd2ae7ea4738',
                activeItem: 'Moscow',
                city: [
                    {
                        key: 5202009,
                        value: 'Moscow',
                    },
                    {
                        key: 703448,
                        value: 'Kyiv'
                    },
                    {
                        key: 703494,
                        value: 'London'
                    }
                ],
            };
        },
        mounted() {
            axios.get(this.url + '?id=' + '5202009' + '&units=metric&appid=' + this.id)
                .then(response => (this.info = response));
        },
        methods: {
            isActive(menuItem) {
                return this.activeItem === menuItem
            },
            setActive(menuItem, key) {
                axios.get(this.url + '?id=' + key + '&units=metric&appid=' + this.id)
                    .then(response => (this.info = response));
                this.activeItem = menuItem
            }
        }
    }
</script>

<style scoped>

</style>