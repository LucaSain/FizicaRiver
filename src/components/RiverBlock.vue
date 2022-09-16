<template>
    <div id="RB-Prebase">
        <div id="RB-Base">
            <div id="RB-River" ref="RBRiver" :style="len">
                <div id="RB-Boat" :style="stl">
                    <div id="RB-Arrow" ref="arr" :style="rotate"></div>
                    <div id="RB-ArrowI" ref="res" :style="suprarotate"></div>
                </div>
                <div id="RB-Where" :style="std"></div>
                
            </div>
        </div>
    </div>
</template>

<script>
import { thisExpression } from '@babel/types';



export default {
    methods:{
        update(){
            this.NewAlpha = this.Alpha * (Math.PI / 180);
            this.htg = this.$refs.RBRiver.clientHeight;
            this.time = this.htg / (this.WSpeed * Math.cos(this.NewAlpha))
            this.oxpos = (this.USpeed - this.WSpeed * Math.sin(this.NewAlpha)) * this.time
            this.oy = this.WSpeed * Math.cos(this.NewAlpha) * this.time
           // this.suprarotate["heigth"]=this.htg/this.Length*Math.sqrt(this.oxpos*this.oxpos+this.oy*this.oy).toString()+ "px"
            //console.log(this.suprarotate["heigth"])
        }
    },
    data() {
        return {
            suprarotate:{

            },
            rotate: {

            },
            std: {

            },
            stl: {

            },
            len: {

            },
            htg: 0,
            time: 0,
            oy: 0,
            oxpos: 0,
            NewAlpha: 0
        }
    },
    props: [
        'Length',
        'XPosDest',
        'USpeed',
        'WSpeed',
        'Alpha',
        'Started'
    ],
    watch: {
        
        Alpha: function (val) {
            this.update()
            let res= Math.atan(this.oxpos/this.oy)
            this.suprarotate={
                "transform":"rotate("+((res/Math.PI *180).toString())+"deg"+")",
                
            }
            this.rotate={
                "transform":"rotate("+(360-this.Alpha).toString()+"deg"+")",

            }
            
        },

        Length: function (val) {
            let lenx = {
                "height": val.toString() + "%" + " !important",
                "margin-top": ((100 - val) / 2).toString() + "%" + " !important"
            };
            this.len = lenx;
            this.update()
        },
        XPosDest: function (val) {
            let wtd = this.$refs.RBRiver.clientWidth;
            this.std = {
                "transform":
                    "translate3d(" + (val * (wtd - (1 / 2) * wtd) / 100).toString() + "px"
                    + ',' + "0"
                    + "px" + ',0px' + ")",
            }
            this.update()
        },


        Started: function (val) {
            this.update()
            let nick;
            if (val) {

                nick = {
                    "transform":
                        "translate3d(" + (this.oxpos).toString() + "px"
                        + ',' + (-1 * this.oy).toString()
                        + "px" + ',0px' + ")",
                    "transition": "all" + " " + this.time.toString() + "s" + " " + "linear",
                };

                this.stl = nick;

            }
            //stop animation
            else {
                nick = {};
                this.stl = nick;
            }
        }
    }
}
</script>

<style scoped>
#RB-ArrowI{
    transform-origin: bottom;
    width: 4px;
    height: 50px;
    background-color: rgb(255, 106, 106);
    margin-left: 43%;
    bottom: 40%;
    position: absolute;
}
#RB-Arrow {
    transform-origin: bottom;
    width: 4px;
    height: 50px;
    background-color: black;
    margin-left: 43%;
    bottom: 40%;
    position: absolute;
}

#RB-Where {

    height: 30px;
    width: 30px;
    background-color: whitesmoke;
    margin-left: 49%;
    border-radius: 100%;
    top: -5%;
    position: absolute;

}

#RB-Prebase {
    margin-top: -1%;
}

#RB-Base {
    background-color: rgb(29, 43, 31);
    color: white;
    height: 101%;
    width: 80%;
    right: 0%;
    position: absolute;
}

#RB-River {
    height: 30%;
    background-color: lightseagreen;
    margin-top: 30%;
    width: 100%;
    position: relative;
}

#RB-Boat {
    height: 30px;
    width: 30px;
    background-color: burlywood;
    margin-left: 49%;
    top: 95%;
    position: absolute;
}
</style>