<template>
    
        <div id = "appMid">
            
            <div id='intro'></div>
            
            <div id="secondBlock">
                <a href="https://www.fanshaweonline.ca/d2l/home"><img src="appImages/fanshawe.jpg" /></a>
                <a href="https://www.healthunit.com/covid-19-cases-middlesex-london"><img src='appImages/london.jfif' /></a>
                <a href="https://www.ontario.ca/page/how-ontario-is-responding-covid-19"><img src='appImages/ontario.jpg' /></a>
                <a href="https://www.facebook.com/"><img src='appImages/facebook.png' /></a>
                <a href="https://www.youtube.com/"><img src='appImages/youtube.png' /></a>
                <a href="https://www.reddit.com/r/londonontario/"><img src='appImages/reddit.png' /></a>
                <a href="https://webadvisor.fanshawec.ca/WebAdvisor/WebAdvisor?TOKENIDX=2052750031&SS=LGRQ&URL=HTTPS%3A%2F%2Fwebadvisor.fanshawec.ca%3A443%2FWebAdvisor%2FWebAdvisor%3FTYPE%3DM%26PID%3DCORE-WBMAIN&CONSTITUENCY=WBST"><img src="appImages/fanshawe.jpg" /></a>
            </div>

            

            <!-- <div id="search">
                <form action="https://www.google.com/search" class="searchform" method="get" name="searchform" target="_blank">
                    <input name="sitesearch" type="hidden" value="">
                    <input autocomplete="on" class="form-control search" name="q" placeholder="Search Google.ca" required="required" type="text">
                </form>
            </div> -->

            <div id="sched">
                <img src="/pic (2).png" alt="Italian Trulli">
            </div>
            
            
        </div>

</template>

<script>
    export default {
        data() {
            return {
                

            }
        },      
        methods:{
            updateIntro() {
                var cityName = "London";
                var today = new Date();
                var hour = today.getHours();

                if (hour >= 6 && hour < 12) {
                    document.getElementById('intro').innerHTML = "Good Morning, " + cityName;
                } else if (hour >= 12 && hour < 17) {
                    document.getElementById('intro').innerHTML = "Good Afternoon, " + cityName;
                } else {
                    document.getElementById('intro').innerHTML = "Good Evening, " + cityName;
                }
            },
            updateWeather() {
                var url = "http://api.openweathermap.org/data/2.5/weather?q=Toronto&appid=8904de5d91911b694079cb1f4abf7d7c";
                fetch(url)
                .then(function(resp) {
                    return resp.json()
                })
                .then(function(data) {
                    var celcius = Math.round(parseFloat(data.main.temp) - 273.15);
                    var feelsLike = Math.round(parseFloat(data.main.feels_like) - 273.15);
                    var imgCode = data.weather[0].icon;

                    document.getElementById("temp").innerHTML = celcius + "° " + data.weather[0].description + ", feels like " + feelsLike + "° ";
                    document.getElementById("tempIMG").src = "http://openweathermap.org/img/wn/" + imgCode + "@2x.png";
                })
            },
            updateNext(){
                                //day,time,classname
                var classesTime=[
                    {dat: "mon",time: 14,names: "Strucutres and Algorithms",when: "2-4"},
                    {dat: "tues",time: 9,names: "Client/Server",when: "9-10"},
                    {dat: "tues",time: 12,names: "Networking",when: "12-1"},
                    {dat: "tues",time: 14,names: "Object Orientated Analysis",when: "2-4"},
                    {dat: "tues",time: 16,names: "Database",when: "4-7"},
                    {dat: "wed",time: 11,names: "CO-OP",when: "11-12"},
                    {dat: "wed",time: 12,names: "Comm for IT",when: "12-1"},
                    {dat: "thurs",time: 9,names: "Networking",when: "9-11"},
                    {dat: "thurs",time: 14,names: "Object Orientated Analysis",when: "2-4"},
                    {dat: "thurs",time: 16,names: "Strucutres and Algorithms",when: "4-6"}
                    ];
            
            
           

                var today = new Date();
                var dayOfWeek = today.getDay();
                var day;
                if(dayOfWeek==1){
                    day = "mon";
                }
                if(dayOfWeek==2){
                    day = "tues";
                }
                if(dayOfWeek==3){
                    day = "wed";
                }
                if(dayOfWeek==4){
                    day = "thurs";
                }
                if(dayOfWeek==5){
                    day = "fri";
                }
                if(dayOfWeek==6){
                    day = "sat";
                }
                if(dayOfWeek==7){
                    day = "sun";
                }
                

                var i = 0;
                var text = ' ';
                var currentHour = today.getHours();
                console.log("right noow: "+day+"\ntime: "+currentHour);
                for (i = 0; i < classesTime.length; i++) {
                    if(classesTime[i].dat==day){
                        if(currentHour<classesTime[i].time){
                            if(((classesTime[i].time)-currentHour)>1){
                                text = "You have "+classesTime[i].names+" within "+((classesTime[i].time)-currentHour)+ " hours from "+classesTime[i].when;
                            }
                            else{
                                text = "You have "+classesTime[i].names+" within "+((classesTime[i].time)-currentHour)+ " hour from "+classesTime[i].when;
                            }
                            
                        }
                    }
                    else{
                        text = "No more class today!";
                    }
                }
                
                document.getElementById('next').innerHTML = text;
            }
        },
        mounted(){
            this.updateIntro()
            this.updateWeather()
            this.updateNext()
        }

    }
</script>

<style scoped>
#sched{
    
    --stroke-pos: 1px;
    --stroke-neg: -1px;
    --stroke-color: rgba(218, 218, 218, 0.9);
    filter: drop-shadow(var(--stroke-pos) 0 0 var(--stroke-color)) 
      drop-shadow(var(--stroke-neg) 0 var(--stroke-color))
      drop-shadow(0 var(--stroke-pos) 0 var(--stroke-color))
      drop-shadow(0 var(--stroke-neg) 0 var(--stroke-color))
      drop-shadow(var(--stroke-pos) var(--stroke-pos) 0 var(--stroke-color)) 
      drop-shadow(var(--stroke-pos) var(--stroke-neg) 0 var(--stroke-color))
      drop-shadow(var(--stroke-neg) var(--stroke-pos) 0 var(--stroke-color))
      drop-shadow(var(--stroke-neg) var(--stroke-neg) 0 var(--stroke-color));  
      user-select: none;  
    
}
#appMid{
    background-image: none!important;
    background-color: rgb(255, 255, 255, 0.6);
    margin-left: 25px!important;
    margin-right: 25px!important;
    padding: 1%;
    width: 50%;
    box-shadow: 8px 8px 15px rgb(87, 87, 87);
    /* border-radius: 15px; */
    text-align: center;
    
    border-color: rgb(255, 255, 255);
}
img{
    width: 85%;
    text-align: center;
    padding: 3%;
    
}
#search input[type=text] {
    height: 50px;
    width: 65%;
    font-size: 150%;
    border-radius: 10px;
    border: 2px solid rgb(163, 163, 163);
    opacity: 87%;
    background-image: url("/search.png");
    background-position: 11px 9px;
    background-repeat: no-repeat;
    background-size: 35px;
    padding-left: 6.5%;
}
#search {
    text-align: center;
    
}
#secondBlock IMG:hover {
    -webkit-filter: drop-shadow(3px 3px 3px rgb(170, 170, 170));
    filter: drop-shadow(3px 3px 3px rgb(170, 170, 170));
    width: 115px;
    height: 115px;
    padding: 0.75%;
}

#secondBlock img {
    margin: auto;
    text-align: center;
    width: 110px;
    height: 110px;
    padding: 1.25%;
    -webkit-filter: drop-shadow(3px 3px 3px #222);
    filter: drop-shadow(3px 3px 3px #222);
    padding-bottom: 1em;
}
#intro {
    text-align: center;
    color: white;
    text-shadow: 5px 0.5px 3px black;
    font-size: 500%;
    font-family: 'Staatliches', cursive;
}

#weatherMain {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
}

#temp {
    font-size: 200%;
    color: white;
    font-family: 'Staatliches', cursive;
    padding-bottom: 0.35%;
    text-shadow: 2px 2px #000000;
}

#tempIMG {
    -webkit-filter: drop-shadow(3px 3px 3px #222);
    filter: drop-shadow(3px 3px 3px #222);
    padding-bottom: 1em;
    width: 70px;
}



</style>