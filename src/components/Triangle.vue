<template>
    <v-layout row>
      <v-flex md4>
        <h3>triangle generator</h3>
        <ul>
          <li class="lines">
            <span>side A :</span>
            <input class="line valLine"  @input="filterAfterChange()" type="number" v-model="lines.lineOne.value"/>

          </li>
          <li class="lines">
            <span>side B :</span>
            <input class="line valLine" type="number" @input="filterAfterChange()" v-model="lines.lineTwo.value"/>
          </li>
          <li class="lines">
             <span>side C :</span>
            <input class="line valLine" type="number" @input="filterAfterChange()" v-model="lines.lineTree.value"/>
          </li>
        </ul>
      </v-flex>
      <v-flex md7 offset-xs0 offset-lg1>
        <v-layout column>
          <v-flex md12>
            <div class="triangle-type">

              <div class="type">type:</div>
              <v-alert :value="alert.value">{{alert.text}}</v-alert>
            </div>
          </v-flex>
          <v-flex md12>
            <div class="triangle-img">
               
              <canvas id="canvas"></canvas>
            </div>
          </v-flex>
        </v-layout>
      </v-flex>
    </v-layout>
</template>
<script>

  export default {
    data() {
      return {
        lines: {
          lineOne: {
            value: 0,
          },
          lineTwo: {
            value: 0,
          },
          lineTree: {
            value: 0,
          }
        },
        alert:{
          text:'',
          value:false
        }
      }
    },
    methods:{
      filterAfterChange(){
        this.draw()
      },
      draw(){

       let a = parseInt(this.lines.lineOne.value),
           b =  parseInt(this.lines.lineTwo.value),
           c =  parseInt(this.lines.lineTree.value);
           this.triangle(a,b,c);

      },
      triangle(a,b,c) {
        let ab = (a + b),
            ac = (a + c),
            bc = (b + c),
            aSqrd = a * a,
            bSqrd = b * b,
            cSqrd = c * c,
            a2b2 = aSqrd + bSqrd,
            a2c2 = aSqrd + cSqrd,
            b2c2 = bSqrd + cSqrd;

        if (a < 0 || b < 0 || c < 0) {
          this.alert.value = true;
          this.alert.text = "illegal";
        }else if(a === 0 || b === 0 || c === 0){
         this.alert.value = true;
         this.alert.text = "a triangle must have 3 sides with positive definate length";

        }else{

          if (ab > c || ac > b || bc > a) {

            if (ab == ac && ac == bc) {
              this.alert.value = true;
              this.alert.text = "Equalateral triangle.";


            }
            if ((ab == ac) != bc || (ac == bc) != ab) {
              this.alert.value = true;
              this.alert.text = "Isosceles triangle.";


            }

            if (ab != ac && ac != bc && bc != ab) {

              if(aSqrd == b2c2 || bSqrd == a2c2 || cSqrd == a2b2){
                this.alert.value = true;
                this.alert.text = "Scalene triangle --> right triangle.";
              }else{
                this.alert.value = true;
                this.alert.text = "Scalene!";
              }


            }
          }
          if (ab < c || ac < b || bc < a) {
            this.alert.value = true;
            this.alert.text = "These 3 sides can not form a triangle.";

          }
        }
      },



    },
    mounted(){
      this.draw()
    }

  }

</script>

 <style>
   ul{
     padding:0;
     margin:0;
   }
   .lines{
     display: block;
     width: 100%;
     overflow: hidden;
     background: rgba(0,0,0,0.1);
     padding: 2px 10px;
     margin: 10px 0;
   }
   .lines span {
     float: left;
     vertical-align: middle;
     margin: 10px 10px 10px 20px;
     display: inline-block;
   }
   .line{
     background: rgba(0,0,0,0.1);
     margin: 10px 0;
     float:left;

   }
   input.valLine{
     background: #444;
     border: none;
     color: #ddd;
     margin-left: 10px;
     vertical-align: middle;
     padding: 0 5px;
     box-shadow: 0px 0px 0px 1px rgba(255,255,255,0.3);
     width:50px;
   }

   .triangle-type{
     background-color: rgba(0,0,0,0.3);
     padding:10px 20px;

   }
   .type{
     padding: 10px 0px;

   }

 </style>



