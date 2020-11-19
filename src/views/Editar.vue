<template>
        <div>
          <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Raza</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="raza" id="raza" v-model="form.raza">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Fecha</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="fecha" id="fecha" v-model="form.fecha">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">Estado</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="estado" id="estado" v-model="form.estado">
                            </div>
                        </div>

                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">Peso</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="peso" id="peso" v-model="form.peso">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">Corporal</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="corporal" id="corporal" v-model="form.corporal">
                              </div>
                        </div>
                    </div>
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">Nacimiento</label>
                       <div class="col-sm-4">
                          <input type="text" class="form-control" name="nacimiento" id="nacimiento" v-model="form.nacimiento">
                       </div>
                    </div>


                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
          <!-- <Footer />   -->
        </div>
    
</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
  name:"Editar",
  components:{
    Header,
    //Footer
  },
  data:function(){
    return {
        form:{
          "id":"",
          "raza" : "",
          "fecha": "", 
          "estado" : "",
          "peso" :"",
           "corporal" : "",
           "nacimiento" : "",
          "token" : "" 
        }
    }
  },
  methods:{
      editar(){
          axios.put("http://localhost/apirest_bovino/bovinos",this.form)
          .then( data =>{
              console.log(data);
               this.$router.push("/dashboard");
          })
      },
      salir(){
        this.$router.push("/dashboard");
      },
      eliminar(){
        var enviar = {
            "id" : this.form.id,
            "token" : this.form.token
        };
        axios.delete("http://localhost/apirest_bovino/bovinos", { headers : enviar})
        .then( datos => {
            console.log(datos);
           this.$router.push("/dashboard");
        });

      }
  },
  mounted:function(){
      this.form.id = this.$route.params.id;
      axios.get("http://localhost/apirest_bovino/bovinos?id="+ this.form.id)
      .then( datos => {
        
        this.form.raza = datos.data[0].raza;
        this.form.fecha = datos.data[0].fecha;
        this.form.estado = datos.data[0].estado;
        this.form.peso = datos.data[0].peso;
        this.form.corporal = datos.data[0].corporal;
        this.form.nacimiento = datos.data[0].nacimiento;
        this.form.token = localStorage.getItem("token");
        console.log(this.form);

      })
     
  }  
}
</script>
<style scoped>
 .left{
   text-align: left;
 };
 .margen{
   margin-left: 15px;
   margin-right: 15px;;
 }
</style>