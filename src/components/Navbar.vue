 <template>
    <div>
      <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <a class="navbar-brand" href="#">Stock Control</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Customer
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                <a class="dropdown-item"><router-link to="/add_client">Add</router-link></a>
                <a class="dropdown-item"><router-link to="/list_client">List</router-link></a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item">Something else here</a>
                </div>
            </li>
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Category
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                <a class="dropdown-item"><router-link to="/add_category">Add</router-link></a>
                <a class="dropdown-item" ><router-link to="/list_category">List</router-link></a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item"><router-link to="/list_card_category">Card</router-link></a>
                </div>
            </li>
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Product
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                <a class="dropdown-item"><router-link to="/add_product">Add</router-link></a>
                <a class="dropdown-item" ><router-link to="/list_product">List</router-link></a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" >Something else here</a>
                </div>
            </li>
            </ul>
        </div>
      </nav>
    </div>
 </template>
 
 
 
