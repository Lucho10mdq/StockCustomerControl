<template>
    <div class="container-fluid">
        <div class="col-12">
           <h1>Add Category</h1>           
       </div> 
       <div class="abs-center">
       <form class="form-horizontal">
           <div class="form-row">
               <div class="form-group col-md-12">
                <input  v-model="description"  class="form-control" placeholder="Description">
              </div>
           </div>
       </form>
       </div>
       <loading :active.sync="isLoading" 
        :can-cancel="true" 
        :is-full-page="fullPage"></loading>
       <div class="row">
            <div class="col-sm-12">
                <div class="text-center">
                <button @click="addCategory"  class="btn btn-success"> Save</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
import Loading from 'vue-loading-overlay';
    // Import stylesheet
import 'vue-loading-overlay/dist/vue-loading.css';
export default {
    data () {
        return {
            description:'',
            isLoading: false,
            fullPage: true
        }
    },
    components: {
        Loading
    },
    methods: {
        addCategory () {
            const app = this
            app.isLoading = true;
            const category = {
                description : app.description
            }
            if (app.description != ''){
                app.isLoading = true;
                 axios.post('http://localhost:8000/api/category', category).then(function (response){
                    if (response.status == 200) {
                        app.$toastr.success("Se agrego correctamente",{
                            theme: "bubble",
                            position: "top-center",
                            duration: 3000
                        })
                    }  
                })
                 this.isLoading = false
            } else {
                app.$toastr.error("Debe ingresar una descripcion !!", {
                    theme: "bubble",
                    position: "top-center",
                    duration: 3000
                })
            }
            app.description = ''
        }
    },
}
</script>

<style scoped>
h1 {
      margin-left: auto;
      margin-right: auto;
      margin-top: 4%;
     text-align: center;
 }
 .form-row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -5px;
    margin-left: -5px;
    margin-top: 30%;
    
}
.abs-center {
  display: flex;
  align-items: center;
  justify-content: center;

}
.btn {
    display: inline-block;
    font-weight: 400;
    color:white;
    text-align: center;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    /*background-color: transparent;*/
    /*border: 1px solid transparent;
        border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: transparent;
        border-left-color: transparent;*/
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    width: 10%;
    margin-top:2%
}
</style>
