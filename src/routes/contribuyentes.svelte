<script>
	import Columnas from '../components/contribuyentes/tablas/Columnas.svelte';
    import Documento from '../components/contribuyentes/tablas/Documento.svelte';
    import ModalEditar     from '../components/ModalEditar.svelte';
    import ModalEliminar from '../components/ModalEliminar.svelte';
    import Paginacion from './../components/Paginacion.svelte';
    import {setContext} from 'svelte';

    const DOCUMENTO_CAMPOS= [
        'Código',
        'D.I.',
        'Numero',
        'RAZON SOCIAL',
        'Dirección',
        'Distrito',
        'Provincia',
        'Departamento',
        'Nacionalidad',
        'Telefono',
        'Categoria',
        'Cuenta',
        'ACCIONES'
    ];
    const DOCUMENTOS_VISIBLES=10;
    const PAGINAS_VISIBLES=5;

    let documentos=[];
    let documentosTotal=0;
    let documentosBuscar='';
    
    let paginaActual=1;
    let paginaTieneAnterior=false;
    let paginaTieneSiguiente=false;
    let paginaSiguiente=null;
    let paginaAnterior=null;
    let paginaTotal=1;

    let arrayPaginasTotal=[];
    let arrayPaginasEnGrupos=[];
    let arrayPaginasVisibles=[];
    let arrayIndicePrimero=0;
    let arrayIndiceUltimo=0;
    let arrayIndiceActual=0;
    

    async function buscar(paramPagina) {
        const response= await fetch(`http://190.41.148.28:2702/api/contribuyentes/tabla?razsoc=${documentosBuscar}&limit=${DOCUMENTOS_VISIBLES}&page=${paramPagina}`);
        const resultado = await response.json();

        if (response.ok) {
            documentos= resultado.docs;
            //console.log("Resultado:", documentos);

            documentosTotal=resultado.totalDocs;
            paginaActual=resultado.page;
            paginaTieneAnterior=resultado.hasPrevPage;
            paginaTieneSiguiente=resultado.hasNextPage;
            paginaAnterior= resultado.prevPage;
            paginaSiguiente= resultado.nextPage;
            paginaTotal= resultado.totalPages;

            arrayPaginasTotal = Array.from({length: paginaTotal}, (x, i) => i+1)
            //console.log("Array Total:",arrayPaginasTotal);

            arrayPaginasEnGrupos=crearArrayPaginasEnGrupos(arrayPaginasTotal, PAGINAS_VISIBLES)
            //console.log("Array en Grupos:",arrayPaginasEnGrupos);
            arrayPaginasTotal=[];
            //console.log("Array Total:",arrayPaginasTotal);
            
            arrayIndiceActual = buscarPaginaEnArray(paginaActual, arrayPaginasEnGrupos, PAGINAS_VISIBLES);
            //console.log("indice:", arrayIndiceActual);
            arrayIndicePrimero=0;
            arrayIndiceUltimo=arrayPaginasEnGrupos.length-1;
            arrayPaginasVisibles=arrayPaginasEnGrupos[arrayIndiceActual];
            //console.log(arrayIndicePrimero,arrayIndiceActual,arrayIndiceUltimo);

            arrayPaginasEnGrupos=[];
            //console.log("Array en Grupos:",arrayPaginasEnGrupos);
        }         
    }   
  
    function buscarPaginaEnArray(paginaABuscar, arrayABuscar, cantidadPag) {
        var indiceEncontrado=0;
        for (let indicePadre = 0; indicePadre < arrayABuscar.length; indicePadre++) {
            const valor = arrayABuscar[indicePadre];
            for (let indiceHijo = 0; indiceHijo < cantidadPag; indiceHijo++) {
                if (valor[indiceHijo]== paginaABuscar) {
                    indiceEncontrado=indicePadre;
                    return indiceEncontrado;
                }
            }
        }
    }

    function crearArrayPaginasEnGrupos(arrayPrincipal, longitudPaginas) {
      let arrayEnFragmentos = [], i; 
      for (i = 0; i <= arrayPrincipal.length-1; i+= longitudPaginas) 
        arrayEnFragmentos.push(arrayPrincipal.slice(i, i + longitudPaginas));
        return arrayEnFragmentos;
    }

    buscar(paginaActual);

    function abrirModal() {
        /*document.getElementById('idVentanaModal').style.display = 'block';*/
        document.getElementById('idModalEditar').style.opacity = '1';
        document.getElementById('idModalEditar').style.visibility = 'visible';

    }

    function cerrarModal() {
        /*document.getElementById('idVentanaModal').style.display = 'none';*/
        document.getElementById('idModalEditar').style.opacity = '0';
        document.getElementById('idModalEditar').style.visibility = 'hidden';
    }

    setContext('open',abrirModal);
    setContext('widthTablet','600px');
    setContext('close',cerrarModal);
</script>

<section  class="ventana">
    <div class="ventana__header">
        <h1 class="ventana__header--title">Contribuyentes</h1>
        <span class="ventana__header--close">X</span>
    </div>
    <div class="ventana__body">
        <div class="ventana__frame">
            <label class="ventana__search-razon-social--key" for="">RAZÓN SOCIAL</label>
            <input type="text" class="ventana__search-razon-social--value-input"
                bind:value={documentosBuscar} 
                on:keyup={({target:{value} })=>buscar(1)}
            >

            <div class="ventana__actions">
                <span class="ventana__button--new" title="Nuevo">
                    <img class="ventana__button--picture" src="img/nuevo.png" alt="">Nuevo
                </span>
            </div>
        </div>

        <div class="ventana__content">
            <Columnas {DOCUMENTO_CAMPOS} />

            {#each documentos as doc}
                <Documento
                    {DOCUMENTO_CAMPOS}                
                    {doc}
                />
            {/each}
        </div>

        {#if documentosTotal>0}
            <Paginacion
                {buscar}
                {arrayIndiceActual} 
                {arrayIndicePrimero}
                {arrayIndiceUltimo} 
                {arrayPaginasVisibles}
                {paginaTieneAnterior}
                {paginaTieneSiguiente}
                {paginaAnterior}
                {paginaActual}
                {paginaSiguiente}
                {paginaTotal}
            />
        {/if}
    </div>
</section>

<ModalEditar />
<ModalEliminar />

<style>
:root{
    --color-borde_separacion_estandar: rgba(156,156,156, .5);
    --color-borde_separacion_td:rgb(220,220,220);
    --color-borde-importes_td:rgb(153,153,153);

    --color-letra-titulo_td:black;
    --color-fondo-dato_td:white;
    --color-fondo-titulo_td:rgba(76, 76, 76,.1);
    --color-letra-dato_td:rgb(76, 76, 76);

    --columna-1-ancho:60px;
    --columna-2-ancho:40px;
    --columna-3-ancho:90px;
    --columna-4-ancho:300px;
    --columna-5-ancho:250px;
    --columna-6-ancho:150px;
    --columna-7-ancho:150px;
    --columna-8-ancho:100px;
    --columna-9-ancho:100px;
    --columna-10-ancho:100px;
    --columna-11-ancho:100px;
    --columna-12-ancho:100px;
    --columna-acciones-ancho:220px;
    --fila-altura: 35px;
} 

/*****************
| PARA CELULARES |
*****************/
.ventana{
    width: 98%;
    margin-left:auto;  margin-right:auto;
    color: black;
    background-color: rgb(255, 235, 205);
}

.ventana__header{
    background-color: rgb(160, 82, 45);
    border: 0px solid #000000; border-radius: 5px 5px 0px 0px;

    display: flex;
    align-items: center;
}

.ventana__header--title{
    padding:5px;
    text-align:center;
    color:#fff;
    font-size:1.3em;
    margin:0;
    text-shadow: rgb(0,0,0) 2px 2px 3px;

    flex: 1 1 auto;
}

.ventana__header--close{
    margin-right: 5px;
    border: 1px solid peru; border-radius: 4px;
    width: 20px;
    color: black;
    background-color: white;
    text-align: center;
    cursor:pointer;
}

.ventana__body{
    color: black;
    padding-bottom: 10px;
}

.ventana__frame {
    margin-top: 10px;
    margin-left: auto; margin-right: auto;
    border:1px solid rgb(208,208,156); border-radius: 4px;
    width: 98%; 
    padding-left: 4px; padding-right: 4px; padding-bottom: 4px;

    display: grid;
   
    grid-template: 
        "titulo    titulo    titulo"   var(--altura-label-celular)
        "input     input     boton"    minmax(var(--altura-input-celular),auto)/
         1fr      1fr        100px;
 }

.ventana__search-razon-social--key {
    grid-area: titulo;
    display: flex; 
    align-items: center; 
    font-weight: bold;
}

.ventana__search-razon-social--value-input{
    grid-area: input;

    padding-left: 5px;
    padding-right: 5px;
    border-radius: 10px;
    border: 1px solid black;
}
.ventana__search-razon-social--value-input:focus {
    border: 1px solid  rgb(204,51,0);
}

.ventana__actions {
    grid-area: boton;

    display: flex;
    justify-content: center;
    align-items: center;
}

.ventana__button--new {
    display: flex;
    align-items: center;
    justify-content: center;

    margin-left: 5px;
    width: 100px;    
    background: rgba(255, 255, 191, .3);
    border: 1px solid rgb(153,153,153);
    border-radius: 5px;
    padding: 5px;
}

.ventana__button--picture {
    height: 22px; width: 22px; margin-right: 5px;
}


.ventana__content {
    margin: 10px auto;
    width: 98%;
    background: white;  
}


/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .ventana__frame {
        padding-top: 4px;

        display: grid;
        align-items: center; 
        grid-template: 
            "titulo    input     boton"    minmax(var(--altura-input-celular),auto)/
            1fr      2fr        100px;
    }

    .ventana__search-razon-social--key {
        
        height: var(--altura-label-tablet);
    }

    .ventana__search-razon-social--value-input{
        height: var(--altura-input-tablet);
    }      
}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .ventana__frame {
        height: 50px;

        display: grid;
        align-items: center; 
        grid-template: 
            "titulo    input     boton"    minmax(var(--altura-input-celular),auto)/
             1fr        5fr        100px;
    }
    
    

    .ventana__search-razon-social--value-input{
        height: var(--altura-input-desktop);
        border-radius: 0;
    }

    .ventana__content {
        overflow-x: scroll;
    }

    .ventana__button--new {
        padding: 2px;
    }
}

</style>