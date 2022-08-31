<script>
	import TablaAcciones from './TablaAcciones.svelte';
    
    export let DOCUMENTO_CAMPOS;
    export let doc;
    
</script>

<div class="tabla__row">
    <div class="tabla__row-header-1 tabla__row-header">{DOCUMENTO_CAMPOS[0]}</div>
    <div class="tabla__data-1 tabla__data">{doc.codigo_interno}</div>

    <div class="tabla__row-header-2 tabla__row-header">{DOCUMENTO_CAMPOS[1]}</div>
    <div class="tabla__data-2 tabla__data">{doc.documento_de_identidad.tipo}</div>

    <div class="tabla__row-header-3 tabla__row-header">{DOCUMENTO_CAMPOS[2]}</div>
    <div class="tabla__data-3 tabla__data">{doc.documento_de_identidad.numero}</div>

    <div class="tabla__row-header-4 tabla__row-header">{DOCUMENTO_CAMPOS[3]}</div>
    <div class="tabla__data-4 tabla__data">{doc.razon_social}</div>

    <div class="tabla__row-header-5 tabla__row-header">{DOCUMENTO_CAMPOS[4]}</div>
    <div class="tabla__data-5 tabla__data">{doc.direcciones[0].direccion}</div>

    <div class="tabla__row-header-6 tabla__row-header">{DOCUMENTO_CAMPOS[5]}</div>
    <div class="tabla__data-6 tabla__data">{doc.direcciones[0].distrito}</div>

    <div class="tabla__row-header-7 tabla__row-header">{DOCUMENTO_CAMPOS[6]}</div>
    <div class="tabla__data-7 tabla__data">{doc.direcciones[0].provincia}</div>

    <div class="tabla__row-header-8 tabla__row-header">{DOCUMENTO_CAMPOS[7]}</div>
    <div class="tabla__data-8 tabla__data">{doc.direcciones[0].departamento}</div>

    <div class="tabla__row-header-9 tabla__row-header">{DOCUMENTO_CAMPOS[8]}</div>
    <div class="tabla__data-9 tabla__data">{doc.nacionalidad}</div>

    <div class="tabla__row-header-10 tabla__row-header">{DOCUMENTO_CAMPOS[9]}</div>
    <div class="tabla__data-10 tabla__data">{doc.medios_de_comunicacion[0].descripcion}</div>

    <div class="tabla__row-header-11 tabla__row-header">{DOCUMENTO_CAMPOS[10]}</div>
    <div class="tabla__data-11 tabla__data">{doc.categoria}</div>

    <div class="tabla__row-header-12 tabla__row-header">{DOCUMENTO_CAMPOS[11]}</div>
    <div class="tabla__data-12 tabla__data">{doc.codigo_contable}</div>

    <TablaAcciones codigo={doc.codigo_interno} />
</div>


<style>
    
/*****************
| PARA CELULARES |
*****************/
.tabla__row {
    background: white;
    border: 1px solid rgb(186,186,186); border-radius: 5px 5px 0px 0px;
    margin-bottom: 0.5em;

    display: grid;
    
    grid-template: 
        "row-header-1    data-1"         var(--altura-label-celular)
        "row-header-2    row-header-2"   var(--altura-label-celular)
        "data-2          data-2"         minmax(var(--altura-input-celular),auto)
        "row-header-3    row-header-3"   var(--altura-label-celular)
        "data-3          data-3"         minmax(var(--altura-input-celular),auto)
        "row-header-4    row-header-4"   var(--altura-label-celular)
        "data-4          data-4"         minmax(var(--altura-input-celular),auto)
        "row-header-5    row-header-5"   var(--altura-label-celular)
        "data-5          data-5"         minmax(var(--altura-input-celular),auto)
        "row-header-6    row-header-6"   var(--altura-label-celular)
        "data-6          data-6"         minmax(var(--altura-input-celular),auto)
        "row-header-7    row-header-7"   var(--altura-label-celular)
        "data-7          data-7"         minmax(var(--altura-input-celular),auto)
        "row-header-8    row-header-8"   var(--altura-label-celular)
        "data-8          data-8"         minmax(var(--altura-input-celular),auto)
        "row-header-9    row-header-9"   var(--altura-label-celular)
        "data-9          data-9"         minmax(var(--altura-input-celular),auto)
        "row-header-10   row-header-10"  var(--altura-label-celular)
        "data-10         data-10"        minmax(var(--altura-input-celular),auto)
        "row-header-11   row-header-11"  var(--altura-label-celular)
        "data-11         data-11"        minmax(var(--altura-input-celular),auto)
        "row-header-12   row-header-12"  var(--altura-label-celular)
        "data-12         data-12"        minmax(var(--altura-input-celular),auto)
        "acciones        acciones"       minmax(var(--altura-button-celular),auto)/
         auto            auto;
}

.tabla__row-header{
    display: flex; 
    align-items: center;
    font-weight: bold;
    padding-left: 5px;
    padding-right: 5px;
    color: rgb(76, 76, 76);
    background-color:var(--color-fondo-titulo_td);
}

.tabla__data{
    display: flex;
    align-items: center;
    padding-left: 5px;
    padding-right: 5px;
    color: rgb(76, 76, 76);
    background-color:var(--color-fondo-dato_td);

    border: 1px solid var(--color-borde_separacion_td);
}

.tabla__row-header-1{
    grid-area: row-header-1;
    border-radius: 5px 0px 0px 0px;

    background-color:rgb(82, 60, 60);
    color: white;

    display: flex; align-items: center;
    flex-direction: row; justify-content: right;
}
.tabla__data-1{
    grid-area: data-1;
    background-color:rgb(82, 60, 60);
    color: white;
    border-radius: 0px 5px 0px 0px;
    border: none;
}

.tabla__row-header-2{grid-area: row-header-2;}
.tabla__data-2{grid-area: data-2;}

.tabla__row-header-3{grid-area: row-header-3;}
.tabla__data-3{grid-area: data-3;}

.tabla__row-header-4{grid-area: row-header-4;}
.tabla__data-4{grid-area: data-4; color: midnightblue;font-weight: bold;}

.tabla__row-header-5{grid-area: row-header-5;}
.tabla__data-5{grid-area: data-5;}

.tabla__row-header-6{grid-area: row-header-6;}
.tabla__data-6{grid-area: data-6;}

.tabla__row-header-7{grid-area: row-header-7;}
.tabla__data-7{grid-area: data-7;}

.tabla__row-header-8{grid-area: row-header-8;}
.tabla__data-8{grid-area: data-8;}

.tabla__row-header-9{grid-area: row-header-9;}
.tabla__data-9{grid-area: data-9;}

.tabla__row-header-10{grid-area: row-header-10;}
.tabla__data-10{grid-area: data-10;}

.tabla__row-header-11{grid-area: row-header-11;}
.tabla__data-11{grid-area: data-11;}

.tabla__row-header-12{grid-area: row-header-12;}
.tabla__data-12{grid-area: data-12;}


/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .tabla__row {
        display: grid;
        
        grid-template: 
            "row-header-1    data-1"   minmax(var(--altura-input-tablet),auto)
            "row-header-2    data-2"   minmax(var(--altura-input-tablet),auto)
            "row-header-3    data-3"   minmax(var(--altura-input-tablet),auto)
            "row-header-4    data-4"   minmax(var(--altura-input-tablet),auto)
            "row-header-5    data-5"   minmax(var(--altura-input-tablet),auto)
            "row-header-6    data-6"   minmax(var(--altura-input-tablet),auto)
            "row-header-7    data-7"   minmax(var(--altura-input-tablet),auto)
            "row-header-8    data-8"   minmax(var(--altura-input-tablet),auto)
            "row-header-9    data-9"   minmax(var(--altura-input-tablet),auto)
            "row-header-10   data-10"  minmax(var(--altura-input-tablet),auto)
            "row-header-11   data-11"  minmax(var(--altura-input-tablet),auto)
            "row-header-12   data-12"  minmax(var(--altura-input-tablet),auto)
            "acciones        acciones" minmax(var(--altura-button-tablet),auto)/
             1fr             2fr;
    }
}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .tabla__row {
        width: 100%;
        margin-bottom: 0;
        border: none; border-radius: 0px 0px 0px 0px;

        display: grid;
        grid-template: 
            "data-1                  data-2                   data-3                   data-4                   data-5                   data-6                   data-7                   data-8                  data-9                   data-10                    data-11                  data-12                   acciones"                       var(--fila-altura)/
            var(--columna-1-ancho)   var(--columna-2-ancho)   var(--columna-3-ancho)   var(--columna-4-ancho)   var(--columna-5-ancho)   var(--columna-6-ancho)   var(--columna-7-ancho)   var(--columna-8-ancho)   var(--columna-9-ancho)   var(--columna-10-ancho)   var(--columna-11-ancho)   var(--columna-12-ancho)  var(--columna-acciones-ancho);
    }

    .tabla__row-header-1{display: none;}
    .tabla__row-header-2{display: none;}
    .tabla__row-header-3{display: none;}
    .tabla__row-header-4{display: none;}
    .tabla__row-header-5{display: none;}
    .tabla__row-header-6{display: none;}
    .tabla__row-header-7{display: none;}
    .tabla__row-header-8{display: none;}
    .tabla__row-header-9{display: none;}
    .tabla__row-header-10{display: none;}
    .tabla__row-header-11{display: none;}
    .tabla__row-header-12{display: none;}

    .tabla__data {
        border: none;
        border-bottom: 1px solid var(--color-borde_separacion_estandar); 
        border-right: 1px solid var(--color-borde_separacion_estandar);            
    }

    .tabla__data-1{
        grid-area: data-1;
        background-color:white; color: black;

        border: none;
        border-left: 1px solid var(--color-borde_separacion_estandar); 
        border-right: 1px solid var(--color-borde_separacion_estandar);    
        border-bottom: 1px solid var(--color-borde_separacion_estandar);    

        border-radius: 0px 0px 0px 0px;
        font-weight: bold;
    }

    .tabla__data:hover {
        background: rgba(222, 222, 160, .5);
        color: black;
    }
}

</style>