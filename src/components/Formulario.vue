<template>

  <section class="src-components-formulario">
      <div class="jumbotron">
        <h2>Formulario</h2>
        <hr>
        <hr>
        <br>
        
        <vue-form :state="formState" @submit.prevent="enviar()">
   
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off" 
            v-model.trim="formData.nombre" 
            name="nombre"
            required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"  
          >        
  
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">El nombre debe poseer al menos {{nombreMinLength}} caracters</div>
            <div slot="minlength" class="alert alert-danger mt-1">El nombre debe poseer como maximo {{nombreMaxLength}} caracters</div>
          </field-messages>
        </validate>
        
        <br>
  
        <validate tag="div">
          <label for="descripcion">Descripción</label>
          <input type="text" 
            id="descripcion" 
            class="form-control" 
            autocomplete="off" 
            v-model.trim="formData.descripcion" 
            name="descripcion"
            required 
            :minlength="descripcionMinLength"
            :maxlength="descripcionMaxLength"  
          >        
  
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">El descripcion debe poseer al menos {{descripcionMinLength}} caracters</div>
            <div slot="minlength" class="alert alert-danger mt-1">El descripcion debe poseer como maximo {{descripcionMaxLength}} caracters</div>
          </field-messages>
        </validate>
  
        <br>
  
        <validate tag="div">
          <label for="monto">Importe</label>
          <input 
            type="number" 
            id="monto" 
            class="form-control" 
            autocomplete="off" 
            v-model.number="formData.monto" 
            name="monto"
            required  
            :min = montoMin
            :max = montoMax
          >        
  
          <field-messages name="monto" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">Debe ser mayor de {{montoMin}}</div>
            <div slot="max" class="alert alert-danger mt-1">Debe ser menor de {{montoMax}}</div>
          </field-messages>
        </validate>
           
        <button class="btn.btn-success.my-3" :disabled="formState.$invalid" type="submit">Enviar</button>
  
        </vue-form>
        
        <br>
        <hr>
        
        <table class="table responsive table-light">
          <tr>
            <th>Nombre</th>
            <th>Descripción</th>
            <th>Importe</th>
            <th>Fecha</th>            
          </tr>
          <tr v-for="(importe,index) in importes" :key="index" >
            <th>{{importe.nombre}}</th>
            <th>{{importe.descripcion}}</th>
            <th> $ {{importe.monto}}</th>
            <th>{{importe.fecha}}</th>            
          </tr>
          <tr>
            <th>Gasto Total</th>
            <th :style = "{color: colorSaldos(sumatoria).color}"> {{sumatoria}} </th>
          </tr>          
        </table>
      </div>
  </section>
     
  </template>

<script>

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {       
        formState: {},
        formData : this.getInitialData(),
        sumatoria: 0,
        importes: [],
        nombreMinLength: 3,
        nombreMaxLength: 15,
        descripcionMinLength: 1,
        descripcionMaxLength: 20,
        montoMin: 1,
        montoMax: 999999        
      }
    },
    methods: {
      getInitialData(){
        return {
        nombre: null,
        descripcion: null,
        monto: null,
        fecha: null     
      }
     },
       enviar(){
      let importe = {...this.formData}
      importe.fecha = new Date().toLocaleString()

      this.importes.push(importe)
      this.sumatoria = this.sumatoria + importe.monto

      this.formData = this.getInitialData()  
      this.formstate._reset()
      },
      colorSaldos(sumatoria){ 
        let color = '#008000' //verde 
                
        if (sumatoria >= 1000 && sumatoria <= 5000) {
          color =  '#FF00FF' //magenta
        } else if (sumatoria > 5000) {
          color = '#FFA500' //naranja 
        } 
        return{
          color
        }
      }
    },    
    computed: {

    }
}

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
