<script>
    let titulo="Peruvian Odyssey";
</script>

<div class="logo">
    <img class="logo__img" src="img/logo-posa.png" alt={titulo}>

    <span class="logo__text">
        {titulo}
    </span>
</div>

<style>
    /*----------------
	| PARA CELULARES |
	----------------*/
    .logo {
        border-bottom: 1px solid rgb(177,124,64);
        color: black;
        padding-top: 5px;
        padding-bottom: 5px;

        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    .logo__img {
        margin-left: 5px;
    }

    .logo__text {
        margin-left: 5px;
        font-size:1.5em; 
    }

    /*--------------
    | PARA TABLET  |
    ---------------*/
    @media (min-width: 600px) {

    }

    /*--------------
	| PARA DESKTOP |
	--------------*/
	@media (min-width: 900px) {
        .logo {
            border: none;
            flex: 1 1 auto;
        }
        .logo__text {
            font-size:1.8em; 
        }
    }
</style>