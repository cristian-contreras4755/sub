
<!--
<template>
<v-card-actions class="justify-center">
  <v-btn>
    dashboar
  </v-btn>
</v-card-actions>
</template>
-->

<template>
  <v-container dense >
    <v-row>
         <v-col>

            <template>
              <v-card
                class="mx-auto"
                max-width="1000"
              >

                         


                <v-card-text>
         <GChart type="BarChart" :data="chartData" :options="chartOptions"/>
             <!-- <GChart type="BarChart" :data="chartData" :options="chartOptions"/>--> 
                </v-card-text>
                <v-card-actions>
                  <v-btn
                    text
                    color="deep-purple accent-4"
                  >
                    Learn More
                  </v-btn>
                </v-card-actions>
              </v-card>
            </template>


        
         </v-col>   
    </v-row>


      <v-row>
        <button @click="repVentasXClientes_convert">convertir</button>
        <button @click="updateData">Click to change data</button>
      </v-row>
   
  </v-container>
</template>


<script>
import { GChart } from "vue-google-charts";
import axios from 'axios'
import { stringify } from 'querystring';

export default {
  components: {
    GChart
  },
  data() {
    return {

      fecha_inicio:'',
      fecha_fin:'',
      moneda:'',
      dataPrueba:[],
     // dataFormateada:[],



      //datos del de chart por defecto
      chartDataHeader: ["Clientes", "Total en ventas."],
      chartDataRows:[]/* [
        ["cristian quicaño contrereras", 1000],
        ["2015", 1170],
        ["2016", 660],
        ["2017", 1030]
      ]*/,
      updatedChartData: [],
      chartOptions: {
        chart: {
          title: "Company Performance",
          subtitle: "Sales, Expenses, and Profit: 2014-2017"
        }
      }
    };
  },
  computed: {
    chartData() {
      return [this.chartDataHeader, ...this.updatedChartData];
    }
  },
  methods: {
    updateData() {
      this.updatedChartData = this.chartDataRows.map(row => {
        return row.map((item, index) => {
       /*
          if (index !== 0) {
            const max = item + 1000;
            const min = 0;
            return Math.floor(Math.random() * (max - min)) + min;
          }*/
          return item;
        });
      });
    },
     repVentasXClientes(){
        let me=this;
          let header={"Authorization":"Bearer "+this.$store.state.token};
          let configuracion={headers:header};
        axios.get('api/Reporte/rpt_ventas_x_clientes',configuracion).then(function(response){
          //me.charData1=response.data;
          //convertir a matriz a partir de json.



        }).catch(function(error){
          console.log(error);
        });
      },

      repVentasXClientes_convert(){


        let me=this;
        /*
          let header={"Authorization":"Bearer "+this.$store.state.token};
          let configuracion={headers:header};
          */
//https://localhost:44397/api/Reporte/rpt_ventas_x_clientes?CadRucs=20160000001&FecIni=2020-01-01&FecFin=2020-04-01&Cd_Mda=02
        axios.get('api/Reporte/rpt_ventas_x_clientes?CadRucs=20160000001&FecIni=2020-01-01&FecFin=2020-04-01&Cd_Mda=02').then(function(response){
            //me.charData1=response.data;
            //console.log(response);
            //console.log(JSON.stringify(response.data));
           //this.dataPrueba=response.data;

        if (response.data!=null){


          response.data.forEach(item=>{
  console.log(item);
           
          //  var tempArray={item.nom_cliente,item.total};

           //this.chartDataRows.push([item.nom_cliente,item.total]);
        // console.log("---->>>>>>>>>>>ingreso");
         this.dataPrueba.push(tempArray);
         

   //console.log("---->>>>>>>>>>>salio");
        //  console.log(this.dataPrueba);

          });
console.log((JSON.stringify( this.dataPrueba)));

     //    console.log(JSON.stringify(this.chartDataRows));

        }

        }).catch(function(error){
         
          alert("error f:"+error);
        });
      }
    
  },

  created() {
    //this.repVentasXClientes_convert();
    //this.updateData();
  }
};


</script>
