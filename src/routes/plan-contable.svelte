<script>
	import Columnas from '../components/contribuyentes/tablas/Columnas.svelte';
    import Documento from '../components/contribuyentes/tablas/Documento.svelte';
    import ModalEditar     from '../components/ModalEditar.svelte';
    import ModalEliminar from '../components/ModalEliminar.svelte';
    
    import Paginacion from './../components/Paginacion.svelte';
    import {setContext} from 'svelte';

    const DOCUMENTO_CAMPOS= [
        'Código',
        'DESCRIPCIÓN',
        'Tipo',
        'Relación',
        'Destino Debe',
        'Destino Haber',
        '%',
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
        /*const response= await fetch(`http://localhost:2702/api/plan-contable/tabla?codigo=${documentosBuscar}&limit=${DOCUMENTOS_VISIBLES}&page=${paramPagina}`);*/
        const response= await fetch(`http://190.41.148.28:2702/api/plan-contable/tabla?codigo=${documentosBuscar}&limit=${DOCUMENTOS_VISIBLES}&page=${paramPagina}`);
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

<div  class="ventana">
    <div class="ventana__header">
        <h1 class="ventana__header--title">Plan Contable</h1>
    </div>

    <div class="ventana__body">
        <div class="ventana__frame">
            <label class="ventana__search--key" for="">Cuenta</label>
            <input type="text" class="ventana__search--value"
                bind:value={documentosBuscar} 
                on:keyup={({target:{value} })=>buscar(1)}
            >

            <div class="ventana__actions">
                <span class="ventana__button" title="Nuevo">
                    <img class="ventana__button--picture" src="img/nuevo.png" alt="">Nuevo
                </span>
            </div>
        </div>

        <div class="tabla__container">
        <table class="tabla">
            <thead class="tabla__head">
                {#each DOCUMENTO_CAMPOS as titulo,index }
                    <th class="tabla__th tabla__th--{index}">{titulo}</th>
                {/each}
            </thead>
            
            <tbody>
            {#each documentos as doc}
                <tr class="tabla__tr">
                    <div class="tabla__tr--title">
                        <img src="img/plan-contable/global.png" class="tabla__tr--image" alt="">    
                    </div>

                    <div class="tabla__tr--data">
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[0]}</div>
                            <div class="tabla__td--value tabla__th--0" style="color: rgb(206,145,91);">{doc.codigo}</div>
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[1]}</div>
                            <div class="tabla__td--value tabla__th--1">{doc.descripcion}</div>     
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[2]}</div>
                            <div class="tabla__td--value tabla__th--2">{doc.tipo}</div>     
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[3]}</div>
                            <div class="tabla__td--value tabla__th--3">{doc.relacion}</div>     
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[4]}</div>
                            <div class="tabla__td--value tabla__th--4" style="color: rgb(189,128,174);">{doc.cuentas_de_destino[0].codigo_debe}</div>     
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[5]}</div>
                            <div class="tabla__td--value tabla__th--5" style="color:rgb(189,128,174);">{doc.cuentas_de_destino[0].codigo_haber}</div>     
                        </td>
                        <td class="tabla__td">
                            <div class="tabla__td--field">{DOCUMENTO_CAMPOS[6]}</div>
                            <div class="tabla__td--value tabla__th--6" style="color:rgb(189,128,174);">{doc.cuentas_de_destino[0].porcentaje}</div>     
                        </td>

                        <td class="tabla__buttons">
                            <button class="tabla__button">
                                <img src="img/editar.png" class="tabla__button--image" alt="">
                                <span class="tabla__button--text">Modificar</span>
                            </button>
                            <button class="tabla__button">
                                <img src="img/eliminar.png" class="tabla__button--image" alt="">
                                <span class="tabla__button--text">Eliminar</span>
                            </button>
                        </td>
                    </div>    
                </tr>
            {/each}
            </tbody>
        </table>
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
</div>


<style>
    
/*****************
| PARA CELULARES |
*****************/
.ventana{
    width: 100%;
    /*height: 100%;*/
    margin-left:auto;  margin-right:auto; 
    background:  var(--ventana-background);
    margin-top: 62px;
}

.ventana__header{
    background-color: var(--ventana-header-background);
    border: 0px solid #000000; border-radius: 5px 5px 0px 0px;

    display: flex;
    align-items: center;
}

.ventana__header--title{
    padding:5px;
    text-align:center;
    color: var(--ventana-header-title-color);
    font-size:1.3em;
    margin:0;
    text-shadow: rgb(0,0,0) 2px 2px 3px;

    flex: 1 1 auto;
}

.ventana__body{
    color: var(--ventana-body-color);
    padding-bottom: 10px;
}

.ventana__frame {
    margin-top: 10px;
    margin-left: auto; margin-right: auto;
    background: var(--ventana-frame-background);
    color: var(--ventana-frame-color);
    border:1px solid var(--ventana-frame-color-border-celular);
    border-radius: 10px;
    width: 98%;
    padding-left: 8px; padding-right: 8px; padding-bottom: 8px;

    display: flex;
    flex-direction: column;
    /*align-items: center;*/
    /*justify-content: center;*/
    /*flex-wrap: wrap;*/
    /*justify-content: space-between;*/
 }

 .ventana__search--key {
    height: var(--tabla-td-field-height-celular);
    /*font-weight: bold;*/

    /*border: 1px solid red;*/
    display: flex; 
    flex-direction: row;
    align-items: center; 
    /*flex-basis: 100%;*/
    /*flex: 1 0 100%;*/
}

.ventana__search--value{
    height: var(--tabla-td-value-height-celular);

    padding-left: 5px;
    padding-right: 5px;
    border-radius: 15px;
    border: 1px solid  var(--ventana-search-value-color-border);
    background: var(--ventana-search-value-background);

    display: flex;
    flex-direction: row;
    align-items: center; 

    /*flex: 1 1 70%;*/
}

.ventana__search--value:hover {
    background: var(--ventana-search-value-hover-background);
}

.ventana__actions {
    display: flex;
    justify-content: center;
    align-items: center;
}

.ventana__button {
    margin-left: 5px;
    height: var(--ventana-button-height-celular);
    background:var(--ventana-button-background);
    color: var(--ventana-button-color);
    border: 1px solid var(--ventana-button-color-border);
    border-radius: 10px;
    padding: 5px;
    margin-top: 10px;
    /*width: 120px;*/

    display: flex;
    align-items: center;
    justify-content: center;
    flex-basis: 100%;
    /*flex: 1 1 30%;*/
}

.ventana__button:hover {
    background: var(--ventana-button-hover-background);
}

.ventana__button--picture {
    height: 22px; width: 22px; margin-right: 5px;
}

.tabla__container {
    width: 98%;
    margin-left: auto;
    margin-right: auto;
}

.tabla {
    width: 100%;
    background:  var(--tabla-background-celular);
}

.tabla__head {
    display: none;
}

.tabla__th {
    display: none;
}

.tabla__tr {
    margin-top: 20px;
    border-radius: 25px 25px 0px 0px;
    border: 1px solid var(--tabla-tr-color-border-celular);
    background: var(--tabla-tr-background-celular);

    display: flex; 
    flex-direction: column;
}

.tabla__tr--title {
    display: flex ;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
 
.tabla__tr--image {
    width: 100px;
    height: 100px;  
}

.tabla__tr--data {
    display: flex;
    flex-direction: column;
}

.tabla__td {
    display: flex;
    flex-direction: column;
}

.tabla__td--field {
    height: var(--tabla-td-field-height-celular);
    background: var(--tabla-td-field-background-celular);
    color: var(--tabla-td-field-color-celular);
    /*font-weight: bold;*/
    border-top: 1px solid var(--tabla-td-color-border-celular);
    border-bottom: 1px solid var(--tabla-td-color-border-celular);
    padding-left: 5px;

    display: flex;
    flex-direction: row;
    align-items: center;
}       

.tabla__td--value {
    height: var(--tabla-td-value-height-celular);
    background: var(--tabla-td-value-background-celular);
    color: var(--tabla-td-value-color-celular);
    padding-left: 5px;
    /*border-right: 1px solid var(--tabla-td-color-border-celular);*/

    display: flex;
    align-items: center;
    flex-direction: row;
}

.tabla__buttons {
    padding: 5px;
    background: var(--tabla-buttons-background-celular);
    border-top: 1px solid var(--tabla-td-color-border-celular);
    border-left: 1px solid var(--tabla-td-color-border-celular);
    border-right: 1px solid var(--tabla-td-color-border-celular);

    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-evenly;
}

.tabla__button {
    padding: 10px;
    height: var(--ventana-button-height-celular);
    background: var(--tabla-button-background-celular);
    color: var(--tabla-button-color-celular);
    border: 1px solid var(--tabla-button-color-border-celular);
    border-radius:5px;

    display: flex;
    align-items: center;
    flex-basis: 120px;
}

.tabla__button:hover {
    background: var(--tabla-button-hover-background-celular);
}


.tabla__button--image {
    width: 22px;
    height: 22px;
}

.tabla__button--text {
    margin-left: 5px;
}


/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .ventana__frame {
        padding-top: 10px;
        padding-bottom: 10px;

        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: space-evenly;
    }

    .ventana__search--key {
        margin-right: 10px;
        height: var(--tabla-td-field-height-tablet);

        flex-basis: initial;
        flex-shrink: 0;
    }

    .ventana__search--value{
        height: var(--tabla-td-value-height-tablet);
        flex-grow: 1;
    }      

    .ventana__button {
        margin-top: 0px;
        height: var(--ventana-button-height-tablet);
        width: 120px;
        /*background:var(--ventana-button-background);
        color: var(--ventana-button-color);*/
    }

    .tabla__tr {
        flex-direction: row;
        align-items: center;
    }

    .tabla__tr--title {
        margin-left: 10px;
        margin-right: 10px;
        border-radius: 50% ; 
        border: none;
        background: rgb(77,77,77);

        flex-direction: column;
    }

    .tabla__tr--image {
        width: 70px;
        height: 70px;  
    }

    .tabla__tr--data {
        margin-top: 13px;
        margin-bottom: 13px;
        margin-right: 13px;
        border-bottom:1px solid var(--tabla-td-color-border-tablet);

        flex-grow: 1;
    }

    .tabla__td {
        flex-direction: row;
        flex-basis: auto;
    }
    
    .tabla__td--field {
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;

        flex-basis: 40%;
        border: none;
        
        border-top: 1px solid var(--tabla-td-color-border-tablet);
        border-left: 1px solid var(--tabla-td-color-border-tablet);
        border-right: 1px solid var(--tabla-td-color-border-tablet);       
    }

    .tabla__td--value {
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        flex-basis: 60%;

        border-top: 1px solid var(--tabla-td-color-border-tablet);
        border-right: 1px solid var(--tabla-td-color-border-tablet);
    }

}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {  
    .ventana {
        width: 99%;
        border-left: 1px solid var(--ventana-header-background);
        border-right: 1px solid var(--ventana-header-background);
        border-bottom: 1px solid var(--ventana-header-background);
        /*margin-top: 5px;*/
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 8px;

        /*box-shadow:0 0 25px 0 rgb(203,106,60);*/
        border: 2px solid rgb(136,59,36);
        border-radius: 10px 10px 0px 0px;
    }

    .ventana__header--title{
        font-size:1.6em;
    }

    .ventana__frame {
        flex-direction: row;
        /*flex-wrap: nowrap;
        justify-content: space-evenly;*/
    }
    
    .ventana__search--key {
        /*border: 1px solid red;*/
    }

    .ventana__search--value{
        height: var(--tabla-td-value-height-desktop);
        border-radius: 0;
        /*border: 1px solid blue;     */
    }

    .ventana__button {
        padding: 2px;
        height: var(--ventana-button-height-desktop);
        /*width: 120px;*/
    }

    .tabla__container {
        overflow-x: auto;
        margin-top: 10px;
    }

    .tabla {
        border-collapse: collapse;
    }

    .tabla__head {
        height: 50px;
        border-top: 1px solid  var(--tabla-td-color-border-desktop);
        border-left: 1px solid  var(--tabla-td-color-border-desktop);
        border-bottom: 1px solid  var(--tabla-td-color-border-desktop);
        background:  var(--tabla-td-field-background-desktop);
        color: var(--tabla-td-field-color-celular);
        padding-left: 32px;
        
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .tabla__th {
        border-right: 1px solid var(--tabla-td-color-border-desktop);
        height: 100%;
        font-weight: normal;
        /*font-weight: bold;*/
        
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .tabla__th--0 {width: 80px;}
    .tabla__th--1 {width: 400px;}
    .tabla__th--2 {width: 100px;}
    .tabla__th--3 {width: 100px;}
    .tabla__th--4 {width: 80px;}
    .tabla__th--5 {width: 80px;}
    .tabla__th--6 {width: 50px;}
    .tabla__th--7 {flex-grow: 1;}

    .tabla__tr {
        margin-top: 0px;
        border-radius: 0px 0px 0px 0px;
        border: none;
        border-left: 1px solid var(--tabla-td-color-border-desktop);
        border-bottom: 1px solid var(--tabla-td-color-border-desktop);
            
        flex-direction: row;
    }

    .tabla__tr--title {
        margin-left: 0px;
        margin-right: 0px;
        background: none;
        /*background: var(--tabla-td-value-background-celular);*/
    }
  
    .tabla__tr--image {
        width: 32px;
        height: 32px;  
    }

    .tabla__tr--data {
        margin-top: 0px;
        margin-bottom: 0px;
        margin-right: 0px;

        border: none;
        flex-direction: row;
        
        border-right: 1px solid var(--tabla-td-color-border-desktop);
    }

    .tabla__td--field {
        display: none;
    }       

    .tabla__td--value {
        flex-direction: row;
        justify-content:flex-start;
        align-items: center;

        flex-basis: 100%;

        border: none;
        border-right: 1px solid var(--tabla-td-color-border-desktop);
    }

    .tabla__td--value:hover {
        background: rgb(77,77,77); /* rgb(32,45,46);*/
        color: rgb(203,203,61); /*) rgb(189,128,174);*/
    }
    
    .tabla__buttons {
        padding: 0px;
        background: var(--tabla-buttons-background-desktop);
        border: 1px solid var(--tabla-buttons-background-desktop);
        flex-basis: 100%;        
    }

    .tabla__button {
        /*padding: 10px;*/
        height: var(--ventana-button-height-desktop);
        width: 120px;
        background: var(--tabla-buttons-background-desktop);
        border: 1px solid var(--tabla-buttons-background-desktop);
    }
}   

</style>