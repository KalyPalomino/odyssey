<script>
    export let DOCUMENTO_CAMPOS;    
</script>

<div class="tabla__headers">
    {#each DOCUMENTO_CAMPOS as campos, indice}
        <div class="tabla__column-header-{indice+1} tabla__column-header">{campos}</div>
    {/each}
</div>

<style>

/*****************
| PARA CELULARES |
*****************/
.tabla__headers {
    display: none;
}


/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .tabla__headers {
        display: none;
    }
}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .tabla__headers {
        width: 100%;
        color: black;

        display: grid;
        grid-template: 
            "column-header-1         column-header-2          column-header-3          column-header-4          column-header-5          column-header-6          column-header-7          column-header-8          column-header-9          column-header-10          column-header-11          column-header-12          acciones"                       var(--fila-altura)/
            var(--columna-1-ancho)   var(--columna-2-ancho)   var(--columna-3-ancho)   var(--columna-4-ancho)   var(--columna-5-ancho)   var(--columna-6-ancho)   var(--columna-7-ancho)   var(--columna-8-ancho)   var(--columna-9-ancho)   var(--columna-10-ancho)   var(--columna-11-ancho)   var(--columna-12-ancho)   var(--columna-acciones-ancho);                
  
    }

    .tabla__column-header{
        display: flex; 
        align-items: center;
        justify-content: center;

        font-weight: bold;
        padding-left: 5px;
        padding-right: 5px;
        color: rgb(76, 76, 76);
        background-color:var(--color-fondo-titulo_td);
        /*border: 1px solid  rgba(156,156,156, .5);*/

        border-top: 1px solid var(--color-borde_separacion_estandar);
        border-bottom: 1px solid var(--color-borde_separacion_estandar); 
        border-right: 1px solid var(--color-borde_separacion_estandar);    
    }

    .tabla__column-header-1{grid-area: column-header-1; border-left: 1px solid  var(--color-borde_separacion_estandar);}
    .tabla__column-header-2{grid-area: column-header-2;}
    .tabla__column-header-3{grid-area: column-header-3;}
    .tabla__column-header-4{grid-area: column-header-4;}
    .tabla__column-header-5{grid-area: column-header-5;}
    .tabla__column-header-6{grid-area: column-header-6;}
    .tabla__column-header-7{grid-area: column-header-7;}
    .tabla__column-header-8{grid-area: column-header-8;}
    .tabla__column-header-9{grid-area: column-header-9;}
    .tabla__column-header-10{grid-area: column-header-10;}
    .tabla__column-header-11{grid-area: column-header-11;}
    .tabla__column-header-12{grid-area: column-header-12;}
}

</style>