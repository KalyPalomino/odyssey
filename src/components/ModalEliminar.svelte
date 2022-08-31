<script>
    import {getContext} from 'svelte';
    import Eliminar from './contribuyentes/tablas/Eliminar.svelte';
    let titulo="Eliminar registro";

    const widthTablet= getContext('widthTablet');
</script>

<svelte:head>
    {@html `
        <style>
            @media (min-width: 600px) {
                .modal__window{
                    width: ${widthTablet};
                }
            }
        </style>
    `}
</svelte:head>

<div id="idModalEliminar" class="modal">
    <div class="modal__window">
        <div class="modal__header">
            {titulo}
        </div>

        <div class="modal__body">
            <Eliminar />
        </div>
    </div>
</div>

<style>

/*****************
| PARA CELULARES |
*****************/
.modal{
    opacity: 0;
    visibility: hidden;

    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100vh;
    background:  rgba(204,204,204,0.8);

    display: flex;
    justify-content: center;
    align-items: center;
}

.modal__window{
    width: 100%;
}

.modal__header{
    margin:0;
    padding:5px;
    text-align:center;
    color:#fff;
    text-shadow: rgb(0,0,0) 2px 2px 3px;
    font-size:1.5em;
    background-color:rgba(153,51,0,0.9);
    border-radius: 10px 10px 0px 0px;
    border: 0px solid #000000;
}

.modal__body{
    padding-left: 10px;
    padding-right: 10px;
    background-color: white; 
    border: 1px solid brown;
}


/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .modal__window{
        width: var(--widthModal);
    }

    .modal__header{
        font-size:1.7em;
    }

    .modal__body{
        min-width: 600px;
    }    

}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .modal__body{
        background-color: rgb(255, 235, 205);
    }

}

</style>

