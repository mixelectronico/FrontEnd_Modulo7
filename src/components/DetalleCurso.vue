<template>
    <div class="rowData">
        <div class="cursoNombre data">
            <span>{{ curso.nombre }}</span>
        </div>
        <div class="cursoCupos data">
            <span>{{ curso.cupos }}</span>
        </div>
        <div class="cursoInscritos data">
            <span>{{ curso.inscritos }}</span>
        </div>
        <div class="cursoDuracion data">
            <span>{{ curso.duracion }}</span>
        </div>
        <div class="cursoCosto data">
            <span v-if="isAString(curso.costo)">$ {{ curso.costo }}</span>
            <span v-else class="badge rounded-pill text-bg-success">$ {{ Number(curso.costo).toLocaleString('es-CL') }}</span>
        </div>
        <div class="cursoTerminado data">
            <span v-if="isAString(curso.completado)">{{ curso.completado }}</span>
            <span v-else-if="curso.completado" class="badge rounded-pill text-bg-primary">Si</span>
            <span v-else class="badge rounded-pill text-bg-secondary">No</span>
        </div>
        <div class="cursoFecha data">
            <span v-if="hasText(curso.fecha_registro, 'FECHA REGISTRO')">{{ curso.fecha_registro }}</span>
            <span v-else class="badge rounded-pill text-bg-success">{{ curso.fecha_registro }}</span>
        </div>
        <div class="cursoAcciones action">
            <span v-if="hasText(curso.acciones, 'ACCIONES')">{{ curso.acciones }}</span>
            <span v-else>
                <svg @click="editar(curso.id)" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-fill edit" viewBox="0 0 16 16">
                    <path d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.5.5 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11z"/>
                </svg>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash-fill delete" viewBox="0 0 16 16">
                    <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5M8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5m3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0"/>
                </svg>
            </span>
        </div>
    </div>
</template>

<script>
export default{
    name: 'CursoData',
    props: {
        curso:{
            type:Object,
            required: true,
        }
    },
    data: function(){
        return{}
    },
    //computed: {},
    methods: {
        isAString(value){
            if(typeof value == "string"){
                return true;
            }else{return false;}
        },
        hasText(value, text){
            if(value === text){
                return true;
            }else{return false;}
        },
        editar(id){
            this.$emit('editarCurso', id);
        }
    },
    //watch: {},
    //components: {},
    //mixins: [],
    //filters: {},
    //-- LifeCycle Methods
    //-- End LifeCycle Methods
}
</script>

<style scoped>
    .badge{
        font-size: 1em;
    }
    .rowData{
        display: flex;
        flex-direction: row;
        column-gap: 1em;
        border-bottom: 1px dotted gray;
        width: fit-content;
    }
    .data{
        margin-block: 8px;
    }
    .action{
        margin-block: 8px;
    }
    .cursoNombre{
        width: 300px;
    }
    .cursoCupos{
        width: 100px;
    }
    .cursoInscritos{
        width: 100px;
    }
    .cursoDuracion{
        width: 100px;
    }
    .cursoCosto{
        width: 100px;
    }
    .cursoTerminado{
        width: 100px;
    }
    .cursoFecha{
        width: 150px;
    }
    .cursoAcciones{
        width: 100px;
    }
    span svg{
        margin-inline: 10px;
    }
    .edit{
        color: var(--bs-warning);
    }
    .delete{
        color: var(--bs-danger);
    }
</style>