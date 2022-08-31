<script>
    import {getContext} from 'svelte';

    let id="";
    let documentoDeIdentidadNumero="";
    let razonSocial="";
    let direccion="";
    let telefono="";

    const LONGITUD_NUMDOCIDE=15, 
          LONGITUD_RAZSOC=100, 
          LONGITUD_DIR=100, 
          LONGITUD_TEL=50;

    const cerrarModal= getContext('close');
</script>


<div class="document-edit__frame">
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Código:</label>
        <input class="document-edit__value--input" type="text" bind:value={id} >
    </div>    
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Documento de identidad:</label>
        <select class="document-edit__value--select" id="idSelRel02_Contri">
        </select>
    </div>
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Número de documento de identidad:
        </label>
        <input class="document-edit__value--input" 
            type="text" 
            bind:value={documentoDeIdentidadNumero} 
            maxlength={LONGITUD_NUMDOCIDE}
        >
    </div>
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">RAZÓN SOCIAL:</label>
        <input class="document-edit__value--input" type="text" 
            bind:value={razonSocial} 
            maxlength={LONGITUD_RAZSOC}
            style="text-transform:uppercase;"  
        >
    </div>
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Tipo:</label>
        <select class="document-edit__value--select" id="idSelRel70_Contri">
            <option value="001">Clientes</option>
            <option value="002">Proveedores</option>
        </select>
    </div>
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Dirección:</label>
        <input class="document-edit__value--input" type="text" 
            bind:value={direccion}
            maxlength={LONGITUD_DIR}
        >
    </div>
        
    <div class="document-edit__group">
        <label class="document-edit__key" for="">Teléfono:</label>
        <input class="document-edit__value--input" type="text" 
            bind:value={telefono}
            maxlength={LONGITUD_TEL}
        >
    </div>

    <!-- ACCIONES -->
    <div class="document-edit__actions">
        <span class="document-edit__button document-edit__button--grabar" on:click={cerrarModal}>
            <img class="document-edit__button--picture" src="img/grabar16x16.png" alt="">
            Grabar
        </span>
        <span class="document-edit__button document-edit__button--cancelar" on:click={cerrarModal}>
            <img class="document-edit__button--picture" src="img/cancelar16x16.png" alt="">
            Cancelar
        </span>
    </div>
</div>


<style>
/*****************
| PARA CELULARES |
*****************/
.document-edit__frame{
    width: 100%;

    display: flex;
    flex-direction: column;
}

.document-edit__group {
    margin-top: 5px;

    display: flex;
    flex-direction: column;
}

.document-edit__key{
    width: 100%;
    height: var(--altura-label-celular); ;
    font-weight: bold;

    display: flex;
    align-items: center;
}

.document-edit__value--input{
    width: 100%; height: var(--altura-input-celular);
    color: rgb(51,51,51);
    padding-left: 5px; padding-right: 5px;
    border: 1px solid peru; border-radius: 5px;
}
.document-edit__value--input:focus {
    border: 1px solid rgb(195,57,18);
    border-radius: 5px;
}

.document-edit__value--select{
    width: 100%; height: var(--altura-input-celular);
    border:1px solid  peru; border-radius: 5px;
    padding-left: 5px; padding-right: 5px;
}
.document-edit__value--select:focus {
    border: 1px solid rgb(195,57,18);
    border-radius: 5px;
}

.document-edit__actions {
    margin-top: 8px;;      
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;

    border: 1px solid #999;
    border-radius: 5px;
    padding-top: 5px;
    padding-bottom: 5px;
    margin-bottom: 10px;
}

.document-edit__button {
    height: var(--altura-button-celular);
    width: 100px;
    background: silver;
    border: 1px solid  #999; border-radius: 15px;
    color:  #000;
    
    display: flex;
    justify-content: center;
    align-items: center; 
}
.document-edit__button:hover {
    background: darkgrey;
}

.document-edit__button--picture {
    height: 22px; width: 22px; margin-right: 5px;
}

/***************
| PARA TABLET  |
***************/
@media (min-width: 600px) {
    .document-edit__frame{
        flex-direction: column;
    }

    .document-edit__group {
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .document-edit__key {
        width: 350px;
        height: var(--altura-label-tablet); 
    }

    .document-edit__value--input {
        height: var(--altura-input-tablet);
    }

    .document-edit__value--select {
        height: var(--altura-input-tablet);
    }

}


/***************
| PARA DESKTOP |
***************/
@media (min-width: 900px) {
    .document-edit__key {
        width: 350px;
        height: var(--altura-label-desktop); 
    }

    .document-edit__value--input {
        height: var(--altura-input-desktop);
        color: rgb(51,51,51);
        border: 1px solid peru; border-radius: 2px;
    }
    .document-edit__value--input:focus {
        border-radius: 2px;
    }

    .document-edit__value--select{
        height: var(--altura-input-desktop);
        border-radius: 2px;
    }
    .document-edit__value--select:focus {
        border-radius: 2px;
    }

    .document-edit__actions {
        border: 1px solid brown;
    }
}

</style>

