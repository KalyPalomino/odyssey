<script>
   import {getContext} from 'svelte';
   export let codigo;
   const abrirModal=getContext('open');

   function modificar() {
     abrirModal();
     console.log('Modificar:',codigo)
   }

   function eliminar() {
    console.log('Eliminar:',codigo)
   }
   
</script>

<div class="tabla__acciones">
    <span title="Modificar" class="acciones__boton acciones__boton--modificar" on:click={modificar}>
        <img class="acciones__imagen" src="img/editar03.png" alt="">Modificar
    </span>
    <span title="Eliminar" class="acciones__boton acciones__boton--eliminar" on:click={eliminar}>
        <img class="acciones__imagen" src="img/eliminar.png" alt="">Eliminar
    </span>
</div>

<style>
/*****************
| PARA CELULARES |
*****************/
.tabla__acciones {
    grid-area: acciones;

    display: flex;
    justify-content: center;
    align-items: center;
}

.acciones__boton {
    display: flex;
    align-items: center;
    justify-content: center;

    width: 100px;    
    background: rgba(255, 255, 191, .3);
    border: 1px solid rgb(153,153,153);
    border-radius: 5px;
    padding: 5px;
}
.acciones__boton--modificar {
    margin-right: 10px;
}
.acciones__boton--eliminar {
    margin-right: 0;
}

.acciones__imagen {
    height: 22px; width: 22px; margin-right: 5px;
}

.acciones__boton:hover{ background: rgba(222, 222, 160, .5);}

/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .acciones__boton {
        margin-top: 0.3em;
        margin-bottom: 0.3em;
    }
}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .tabla__acciones {
        justify-content: space-evenly;
  
        margin-bottom: 0;
        margin-top: 0;

        border-right: 1px solid var(--color-borde_separacion_estandar);    
        border-bottom: 1px solid var(--color-borde_separacion_estandar); 
    }

    .acciones__boton {
        padding: 2px;
        width: 90px;   
    }

    .acciones__boton--modificar {
        margin-right: 0;
    }
}

</style>