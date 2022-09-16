<template>
  <div id="SideBar-Pre">
    <div id="SideBar-Base">
      <div id="SideBar-Root">
        <h1>Simulare :D</h1>
        <h1>Configuratie:</h1>
        <h2>Latime Rau: {{Length}}</h2>
        <input v-model="Length" type="range" name="LControl" id="SideBar-LControl" class="SideBar-Input-Range">
        <h2>Pozitie Destinatie: {{XPosDest}}</h2>
        <input v-model="XPosDest" min="-100" max="100" type="range" name="XControl" id="SideBar-XControl" class="SideBar-Input-Range">
        <h2>Viteza Transport: {{USpeed/10}}</h2>
        <input v-model="USpeed" type="range" name="USpeedControl" id="SideBar-USpeedControl" class="SideBar-Input-Range">
        <h2>Viteza Relativa: {{WSpeed/10}}</h2>
        <input v-model="WSpeed" type="range" name="WSpeedControl" id="SideBar-WSpeedControl" class="SideBar-Input-Range">
        <h2>Unghi Viteza Relativa </h2>
        <div class="SideBar-AlphaRoot">
        <input v-model="Alpha" type="text" name="AlphaControl" id="SideBar-AlphaControl" class="SideBar-Input">
        </div>
        <button @click="Startx">{{Startup}}</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data(){
      return{
        Length:30,
        XPosDest:0,
        USpeed:12,
        WSpeed:10,
        Alpha:90,
        Begin:0,
        Startup:"Start Animatie"
      }
    },
    watch:{
      Length: function(val,oldval){
        this.$emit("LengthCh",this.Length);
      },
      XPosDest: function(val,oldval){
        this.$emit("XPosDestCh",this.XPosDest);
      },
      USpeed: function(val,oldval){
        this.$emit("USpeedCh",this.USpeed);
      },
      WSpeed: function(val,oldval){
        this.$emit("WSpeedCh",this.WSpeed);
      },
      Alpha: function(val,oldval){
        this.$emit("AlphaCh",this.Alpha);
      }
    },
    methods:
    {
      Startx()
      {
        this.Begin=!this.Begin;
        if(this.Begin){
          this.Startup="Reset Animatie"
          
        }
        else{
          this.Startup="Start Animatie"
        }
        this.$emit("StartCh", this.Begin)
      },
    }
  }
</script>

<style scooped>
  .SideBar-Deg{
    position: absolute;
    margin-right: 0;
    margin-top:0;
  }
  .SideBar-Input{
    padding: 7%;
    width:30%;
    font-size: large;
  }
  .SideBar-Input-Range{
    margin-top:-10%;
    width:90%;
    
  }
  #SideBar-Pre{
    margin-left: -1%;
    margin-top:-1%
  }
  #SideBar-Root{
    margin-left:5%;
    margin-top:5%;
  }
  #SideBar-Base{
    height: 101%;
    width: 21%;
    background-color: rgb(47, 79, 58);
    color:white;
    position: absolute;
  }

</style>