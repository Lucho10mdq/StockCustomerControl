<template>
    <div class="container-fluid">
        <div class="col-12">
           <h1>Add Product</h1>           
       </div> 
       <div class="abs-center">
            <form class="form-horizontal">
                <div class="form-row">
                <div class="form-group col-md-4">
                    <select v-model="Category" class="form-control">
                    <option value="0" disabled>Seleccione</option>
                        <option v-for="listCategory in ListCategory" :key="listCategory.id" :value="listCategory.id" v-text="listCategory.description">
                    </option>
                    </select>
                </div>
                <div class="form-group col-md-4">
                    <input v-model="description" class="form-control"  placeholder="Description">
                </div>
                <div class="form-group col-md-4">
                    <input v-model="price" class="form-control"  placeholder="Price">
                </div>
                <div class="form-group col-md-4">
                    <input v-model="code" class="form-control"  placeholder="codigo">
                </div>
                <div class="form-group col-md-4">
                    <input v-model="stock" class="form-control"  placeholder="stock">
                </div>  
                </div>
            </form>
        </div>
         <loading :active.sync="isLoading" 
        :can-cancel="true" 
        :is-full-page="fullPage"></loading>
        <div class="row">
            <div class="col-md-12">
                <div class="text-center">
                <button @click="AddProduct"  class="btn btn-success"> Save</button>
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
            description : '',
            stock :'',
            price: '',
            code: '',
            Category : '0',
            ListCategory : [],
            isLoading: false,
            fullPage: true
        }
    },
    components: {
        Loading
    },
    methods: {
        listCategory () {
            const app = this
            axios.get('http://localhost:8000/api/category').then(function (response){
                app.ListCategory = response.data.Category
                console.log(app.ListCategory)
            })
        },
        AddProduct () {
            const app = this
            app.isLoading = true
            const Product = {
                description : app.description,
                stock : app.stock,
                price : app.price,
                codigo : app.code,
                idCategory: app.Category,
            }
            console.log(Product)
            if ((app.description != '') && (app.stock != '') && (app.price != '')  && (app.code != '') && (app.Category != '') ){
                axios.post('http://localhost:8000/api/product',Product).then(function (response) {
                    if (response.status == 200 ) {
                         app.$toastr.success("Se agrego correctamente", {
                            theme: "bubble",
                            position: "top-center",
                            duration: 3000
                        }) 
                    }
                 })
            } else {
                app.$toastr.error("Debe llenar los campos vacios !!", {
                    theme: "bubble",
                    position: "top-center",
                    duration: 3000
                })
            }
             this.isLoading = false
             app.description = '',
             app.stock = '',
             app.price = '',
             app.code = '',
             app.Category = ''
        }
    },
    mounted() {
        this.listCategory();
    }
}
</script>
<style>
 h1 {
      margin-left: auto;
      margin-right: auto;
      margin-top: 4%;
     text-align: center;
 }
 button{
     float: none;
     text-align: center;
     margin-left: auto;
    margin-right: auto;
 }
 .form-row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -5px;
    margin-left: -5px;
    margin-top: 4%;
}
.abs-center {
  display: flex;
  align-items: center;
  justify-content: center;

}
</style>