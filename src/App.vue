<template>
  <div id="app">

    
    <div id="weatherMain">
            <img id="tempIMG">
            <span id="temp"></span>
            <span id='next'></span>
            <!-- <clock /> -->
            
    </div>
        
    <div id ="comp">
      <mainBoard/>
      <midPanel/>
      
    </div>

    
  </div>
</template>

<script>
// import clock from './components/clock.vue'
import mainBoard from './components/mainBoard.vue'
import midPanel from './components/midPanel.vue'

export default {
  name: 'App',
  components: {
    // clock,
    mainBoard,
    midPanel
  },
  methods:{

    equal(){
     
    }


  }
  
}
</script>

<style scoped>
  
  #app{
    user-select: none;
    background-image: url("/back.jpg");
    background-repeat: repeat;
    background-position-y: -200px;
    background-size: cover;
  }
  #comp{
    display: flex;
    flex-direction:row;
    margin: auto!important;
    text-align: center;
    justify-content: center;
    
  }
#weatherMain {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: left;
    width: 75%!important;
    margin-left:14.2%;
    opacity: 95%;
    padding: 0%!important;
   
}
#next{
  font-size:125%;
  padding-top: 6.4%;
  font-weight: bold;
  color:white;
  text-align: right!important;
  width: 68.8%;
  font-family: 'Roboto', sans-serif;
  text-shadow: 1px 2px #000000;
}
#temp {
    font-size: 200%;
    color: white;
    font-family: 'Staatliches', cursive;
    padding-top: 5.9%;
    text-shadow: 2px 2px #000000;
}

#tempIMG {
    -webkit-filter: drop-shadow(3px 3px 3px #222);
    filter: drop-shadow(3px 3px 3px #222);
    width: 70px;
    padding-top: 5.7%;
}

@media only screen and (max-width: 2000px) {
      #next{
    font-size:125%;
    padding-top: 7.1%;
    font-weight: bold;
    color:white;
    text-align: right!important;
    width: 72%;
    font-family: 'Roboto', sans-serif;
    text-shadow: 1px 2px #000000;
  }
#weatherMain {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: left;
    width: 75%!important;
    margin-left:11%;
    opacity: 95%;
    padding: 0%!important;
   
}
}


</style>
