<template>
    <div id="app">
        <h1>{{ date }}</h1>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                date: null
            }
            
        },
        
        methods: {
            updateTime() {
                var today = new Date();
                var hour = today.getHours();
                var hours;
                if (hour > 12) {
                    hour = hour - 12;
                    hours = " pm";
                } else {
                    hours = " am";
                }
                var mins = today.getMinutes();
                if (mins < 10) {
                    mins = "0" + mins;
                }
                var secs = today.getSeconds();
                if (secs < 10) {
                    secs = "0" + secs;
                }
                var time = hour + ":" + mins + ":" + secs;
                this.date = time+hours;
            }

        },

        created(){
            this.updateTime()
            setInterval(this.updateTime, 1000);
        }
    }
</script>

<style scoped>

#app{
    font-size: 20px;
    
    text-align: left!important;
    color: white;
    background-image: none!important;
    opacity: 50%;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;

    
    
}
</style>