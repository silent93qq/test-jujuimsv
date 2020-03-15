<template>
    <div>
        <div id="app">
            <div class="container-fluid">
                <div class="row justify-content-center">
                    <Weathermap></Weathermap>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Weathermap from "./components/Weathermap";

    export default {
        name: 'App',
        components: {
            Weathermap,
        },

    }
</script>

<style>

</style>
