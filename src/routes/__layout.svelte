<script>
    
</script>


<div class="container">
    <header class="container-header">
        <div class="logo">
			<img class="logo__img" src="img/logo-posa.png" alt="">
            <span class="logo__text">ContiFire</span>
		</div>
			
        <div class="perfil">
            <img class="perfil__img" src="img/perfil/dulce.jpg" alt="">

            <span class="perfil__text">
				Jose Luis Palomino
			</span>

            <img class="perfil__dropdown" src="img/perfil/menu-hamburguesa.png" alt="">

			<div class="perfil__submenu"> 
				<ul>
					<li class="perfil__submen-item">
						<a class="perfil__submen-item-link" href="#">
							<img class="perfil__submen-item-link-img" src="img/perfil/editar-sesion.png" alt="" >
							<span class="perfil__submen-item-link-text">Editar</span>
						</a>
					</li>

					<li class="perfil__submen-item">
						<a class="perfil__submen-item-link" href="#">
							<img class="perfil__submen-item-link-img" src="img/perfil/cerrar-sesion.png" alt="">
							<div class="perfil__submen-item-link-text">Cerrar sesión</div>
						</a>
					</li>
				</ul>
			</div>
        </div>

	
		<div class="empresa">
            20101887414-PERUVIANODYSSEY S.A-2022
		</div>

		<nav class="nav">
			<!-- INICIO DE MENU-TABLAS -->
			<ul class="menu">
				<img class="menu__img" src="img/menu/movchegirlim16x16.png" alt="">
				<span class="menu__text">Tablas	</span>

				<div class="menu__submenu"> 
					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabcodtab.png" alt="" >
							<span class="menu__submen-item-link-text">Código de tablas</span>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabdettab.png" alt="">
							<div class="menu__submen-item-link-text">Detalle de tablas</div>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabplacon.png" alt="">
							<div class="menu__submen-item-link-text">Plan contable</div>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabcontri.png" alt="">
							<div class="menu__submen-item-link-text">Contribuyentes</div>
						</a>
					</li>
				</div>
			</ul>

			<!-- INICIO DE MENU-MOVIMIENTOS -->
			<ul class="menu">
				<img class="menu__img" src="img/menu/replibbancus16x16.png" alt="">
				<span class="menu__text">Movimientos</span>


				<div class="menu__submenu"> 
					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabcodtab.png" alt="" >
							<span class="menu__submen-item-link-text">Movimientos de compras</span>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabdettab.png" alt="">
							<div class="menu__submen-item-link-text">Movimientos de ventas</div>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabplacon.png" alt="">
							<div class="menu__submen-item-link-text">Movimientos de honorarios</div>
						</a>
					</li>
				</div>
			</ul>

			<!-- INICIO DE MENU-REPORTES -->
			<ul class="menu">
				<img class="menu__img" src="img/menu/movhoncus16x16.png" alt="">
				<span class="menu__text">Reportes</span>

				<div class="menu__submenu"> 
					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabcodtab.png" alt="" >
							<span class="menu__submen-item-link-text">Registro de ventas</span>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabdettab.png" alt="">
							<div class="menu__submen-item-link-text">Registro de compras</div>
						</a>
					</li>

					<li class="menu__submen-item">
						<a class="menu__submen-item-link" href="#">
							<img class="menu__submen-item-link-img" src="img/menu/tabplacon.png" alt="">
							<div class="menu__submen-item-link-text">Libro diario</div>
						</a>
					</li>
				</div>
			</ul>
		</nav>
    </header>
    


    <slot></slot>
</div>


<style>

.container {
    height: 100%;
    background-image: url("../img/fondo01.png");
    display: flex;
    flex-direction: column;
}

.container-header {
    display: flex;
    flex-direction: row;  

    position: sticky; 
    top: 0;
    width: 100%;
}

.logo {
    background-image: url("../img/fondo01.png");
    padding-top: 5px;
    padding-bottom: 5px;

    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex: 1 1 auto;
}

.logo__img {
    margin-left: 5px;
}

.logo__text {
    text-shadow: rgb(0,0,0) 2px 2px 4px;
    margin-left: 5px;
    font-size:1.8em; 
}


.perfil {
    background-image: url("../img/fondo01.png");

    display: flex;
    flex-direction: row;
    align-items: center;
}

.perfil__img {
    height: 50px;
    width: 50px;
    border-radius: 50%;
    margin-left: 4px;
    margin-right: 4px;

    display: flex;
    flex-direction: column;
}
           
.perfil__text {
    color: black;
    margin-left: 4px;
    display: none;
} 

.perfil__dropdown{
    height: 30px;
    width: 30px;
    margin-left: 4px;
    border: 1px solid  rgb(82, 60, 60); border-radius: 3px;
    display: none;
}

.perfil__submenu{
    background-color: rgb(255, 235, 205);
    border: 2px solid rgb(205, 133, 63); border-radius: 4px;
    box-shadow: 2px 8px 16px 2px rgba(0,0,0,0.2);
    position: fixed;
    top: 60px; right: 1px;
    z-index: 120;
    min-width: 130px;
    display: none;
}
            
.perfil__submen-item{
    position: relative;
}
            
.perfil__submen-item-link {
    color: black;
    padding-top: 5px; padding-bottom: 5px;

    display: flex;
    flex-direction: row;
    align-items: center;
}
                    
.perfil__submen-item-link-img {
    margin-left: 5px;
    width: 16px;
    height: 16px;
}

.perfil__submen-item-link-text {
    margin-left: 5px; margin-right: 5px;
}

.perfil__submen-item-link:hover {	
    background-color: rgb(160, 82, 45); color: white;
}
        
.perfil:hover {	
    background-color: rgb(82, 60, 60); 
}

/*--- HOVER PARA MOSTRAR EL MENU--- */
.perfil:hover .perfil__submenu {	
    display: block;
}		

.empresa {
    position: fixed; 
    top: 60px;
    width: 100%;
    z-index: 100;
    font-size:1.2em;
    background:rgb(82, 60, 60);
    color: white;
    /*height: 30px; line-height: 28px;*/
    padding-top: 5px; padding-bottom: 5px;

    
    display: flex;
    align-items: center;
    justify-content: center;
}


.nav {
	background-color: rgb(245,225,206); /*rgb(255, 235, 205);*/
    color: black;
    border: 1px solid rgb(205, 133, 63);
    /*padding-top: 5px; padding-bottom: 5px;*/

    /*height: 30px; line-height: 28px;*/
    position: fixed; 
    top: 90px;
    width: 100%;
    z-index: 110;

    display: flex;
    flex-direction: row;
}

.menu {
    margin-top: 3px;
    margin-bottom: 3px;
    margin-left: 3px;

    display: flex;
    flex-direction: row;
    align-items: center;
    padding-top: 5px; padding-bottom: 5px;
}
.menu__img {
    margin-left: 5px;
}

.menu__text {
    margin-left: 2px;
    padding-right: 5px;
}

.menu__submenu{
    background-color: rgb(255, 235, 205);
    
    border: 1px solid rgb(205, 133, 63); border-radius: 4px;
    box-shadow: 2px 8px 16px 2px rgba(0,0,0,0.2);
    /*text-align: left;*/
    position: absolute;
    top: 34px; 
    left: 1px; width: 98%;
         
    display: none;
}

.menu__submen-item{
    position: relative;
    /*height: 30px; line-height: 28px;*/
}

.menu__submen-item-link {
    color: black;
    padding-top: 5px; padding-bottom: 5px;

    display: flex;
    flex-direction: row;
    align-items: center;
}

.menu__submen-item-link-img {
    margin-left: 5px;
}

.menu__submen-item-link-text {
    margin-left: 5px;
}

.menu__submen-item-link:hover {	
    /*background-color: rgb(160, 82, 45); color: white;*/
    background-color: rgb(122, 92, 60); color: white;
}

.menu:hover {
    background-color: rgb(160, 82, 45);
    color: white;
    border-radius: 4px;
    /*margin-top: 2px;
    margin-bottom: 2px;*/
}    

/*--- HOVER PARA MOSTRAR EL SUBMENU--- */
.menu:hover .menu__submenu {	
    display: block;
}			




</style> 