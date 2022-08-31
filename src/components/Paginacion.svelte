<script>
    export let buscar;

    export let arrayIndiceActual;
    export let arrayIndicePrimero;
    export let arrayIndiceUltimo;
    export let arrayPaginasVisibles;
    
    export let paginaTieneAnterior;
    export let paginaTieneSiguiente;
    
    export let paginaAnterior;
    export let paginaActual;
    export let paginaSiguiente;
    export let paginaTotal;
</script>

<div class="paginacion">
    <div 
        class="pagina__anterior {paginaTieneAnterior? '': 'disabled'} "
        on:click={buscar(paginaAnterior)}
        >&lt;
    </div>    
                
    {#if arrayIndiceActual>arrayIndicePrimero}
        <div 
            class="pagina__numero"
            on:click={buscar(1)}>
            {1}
        </div>
        <div class="pagina__desactivada" disabled>
            ...
        </div>
    {/if}

    {#each arrayPaginasVisibles as pag}
        <div 
            class="pagina__numero {(paginaActual === pag) ? 'pagina__actual':''} " 
            on:click={buscar(pag)}>{pag}
        </div>
    {/each}

    {#if arrayIndiceActual<arrayIndiceUltimo}
        <div class="pagina__desactivada" disabled>
            ...
        </div>

        <div 
            class="pagina__numero" 
            on:click={buscar(paginaTotal)}>{paginaTotal}
        </div>
    {/if}

    <div 
        class="pagina__siguiente {paginaTieneSiguiente? '': 'disabled'} "
        on:click={buscar(paginaSiguiente)}
        >&gt;
    </div>    
</div>

<style>
/*****************
| PARA CELULARES |
*****************/
.paginacion{
    display:flex;
    flex-direction: row;
    justify-content: center;
}

.pagina__anterior{
    width: 30px;
    padding: 5px;
    background-color: rgba(76, 76, 76, .4);
    border: 1px solid rgba(76, 76, 76, .6);
    border-radius: 5px;
    font-size: 16px;
    margin-right: 3px;

    display: flex;
    align-items:center;
    justify-content: center;
}
.pagina__numero {
    width: 36px;
    padding: 5px;
    /*border: 1px solid  peru ;*/
    border: 1px solid rgba(55, 10, 10, 1);
    border-radius: 5px;
    margin-right: 3px;

    display: flex;
    align-items:center;
    justify-content: center;
}

.pagina__actual {
    background-color: rgba(55, 10, 10, 1);
    color: #fff;
    border-radius: 5px;
}
    
.pagina__desactivada {
    width: 15px;
    /*border: 1px solid  peru ;*/
    margin-right: 3px;

    display: flex;
    align-items:center;
    justify-content: center;
}

.pagina__siguiente{
    width: 30px;
    padding: 5px;
    background-color: rgba(76, 76, 76, .4);
    border: 1px solid  rgba(76, 76, 76, .6);
    border-radius: 5px;
    font-size: 16px;

    display: flex;
    align-items:center;
    justify-content: center;
}

/***************
| PARA TABLET  |
***************/
/*
@media (min-width: 600px) {

}
*/

/***************
| PARA DESKTOP |
***************/
/*
@media (min-width: 900px) {

}
*/

</style>