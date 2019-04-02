<template>
    <div class="container">
        <div class="col-12">
            <h1>Cards Categories</h1>           
        </div>
        <div class="contenido">
            <div class="row">
                <div v-for="Category in listCategories" :key="Category.id" class="card" style="width: 18rem;">
                    <div class="card-body col-md-12 ">
                            <h5 class="card-title">{{Category.description}}</h5>
                            <h6 class="card-subtitle md-2 text-muted">Card subtitle</h6>
                            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                            <button type="button" class="btn btn-primary"><router-link to="/list_product">View Product</router-link></button>
                            <button type="button" class="btn btn-primary"><router-link to="/add_product">Add Product</router-link></button>  
                    </div>
                </div>
            </div>    
        </div>    
    </div>    
</template>
<script>
import axios from 'axios'
export default {
    data () {
        return {
            listCategories : [],
            description:'',
            searchCustomer: []
        }
    },
    methods: {
        listCategory () {
            const app = this
            axios.get('http://localhost:8000/api/category').then(function (response){
                app.listCategories = response.data.Category
                console.log(app.listCategories)
            })
        },
    },
    mounted() {
        this.listCategory()
    },
}
</script>
<style>
h1 {
      margin-left: auto;
      margin-right: auto;
      margin-top: 4%;
     text-align: center;
 }
 contenido{
     margin: 5%;
     margin-top: 4%
 }
 .card {
    word-wrap: break-word;
    margin-top: 5%;
    padding: 2%;
    border-top: 4px solid blue;
    margin-right: auto;
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
    /*background-color: transparent;
    border: 1px solid transparent;
        border-top-color: transparent;
        border-right-color: transparent;
        border-bottom-color: transparent;
        border-left-color: transparent;*/
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    margin-top:5%;
    margin-left: 12%
}

/*a:hover {
    color: white;
    text-decoration: underline;
}*/

.btn-primary:hover {
    color: white;
    background-color: white;
    border-color: #0062cc;
}

.btn-primary {
    color: white;
    background-color: white;
    border-color: #007bff;
}
</style>
