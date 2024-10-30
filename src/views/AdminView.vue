<template>
    <div class="admin">
        <h1 class="my-4">Administración</h1>
        <button type="button" class="btn btn-primary mb-4" @click="agregarCurso()">AGREGAR CURSO</button>
        <dialog :open="mostrarModal">
            <h1 v-if="modalNuevo">Añade un nuevo Curso</h1>
            <h1 v-else>Edita el curso</h1>
            <input v-model="dialogNombre" class="form-control my-2" type="text" placeholder="Nombre" aria-label="Nombre">
            <input v-model="dialogIMG" class="form-control my-2" type="text" placeholder="URL de la Imagen" aria-label="URL de la Imagen">
            <input v-model="dialogCupos" class="form-control my-2" type="text" placeholder="Cupos del curso" aria-label="Cupos del curso">
            <input v-model="dialogInscritos" class="form-control my-2" type="text" placeholder="Inscritos en el curso" aria-label="Inscritos en el curso">
            <input v-model="dialogDuracion" class="form-control my-2" type="text" placeholder="Duracion del curso" aria-label="Duracion del curso">
            <input v-model="dialogFecha" class="form-control my-2" type="text" placeholder="Fecha de registro" aria-label="Fecha de registro">
            <input v-model="dialogCosto" class="form-control my-2" type="text" placeholder="Costo del curso" aria-label="Costo del curso">
            <label class="form-label">Descripción</label>
            <textarea v-model="dialogDescripcion" class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
            <button type="button" class="btn btn-success mx-2 my-4">AGREGAR</button>
            <button type="button" class="btn btn-warning mx-2 my-4" @click="limpiarFormulario()">LIMPIAR FORMULARIO</button>
            <button type="button" class="btn btn-danger mx-2 my-4" @click="ocultarModal()">CANCELAR</button>
        </dialog>
        <section>
            <DetalleCurso :curso="cabecera"/>
            <DetalleCurso v-on="editarCurso" v-for="curso in cursos" :key="curso.id" :curso="curso"/>
        </section>
        <footer class="container">
            <div class="alert permitidos">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-people-fill" viewBox="0 0 16 16">
                    <path d="M7 14s-1 0-1-1 1-4 5-4 5 3 5 4-1 1-1 1zm4-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6m-5.784 6A2.24 2.24 0 0 1 5 13c0-1.355.68-2.75 1.936-3.72A6.3 6.3 0 0 0 5 9c-4 0-5 3-5 4s1 1 1 1zM4.5 8a2.5 2.5 0 1 0 0-5 2.5 2.5 0 0 0 0 5"/>
                </svg>
                Cantidad total de alumnos permitidos: {{ totalAlumnosPermitidos }} alumnos.
            </div>
            <div class="alert inscritos">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-person-fill-check" viewBox="0 0 16 16">
                    <path d="M12.5 16a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7m1.679-4.493-1.335 2.226a.75.75 0 0 1-1.174.144l-.774-.773a.5.5 0 0 1 .708-.708l.547.548 1.17-1.951a.5.5 0 1 1 .858.514M11 5a3 3 0 1 1-6 0 3 3 0 0 1 6 0"/>
                <path d="M2 13c0 1 1 1 1 1h5.256A4.5 4.5 0 0 1 8 12.5a4.5 4.5 0 0 1 1.544-3.393Q8.844 9.002 8 9c-5 0-6 3-6 4"/>
                </svg>
                Cantidad total de alumnos inscritos: {{ totalAlumnosInscritos }} alumnos.
            </div>
            <div class="alert restantes">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-person-plus-fill" viewBox="0 0 16 16">
                    <path d="M1 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6"/>
                    <path fill-rule="evenodd" d="M13.5 5a.5.5 0 0 1 .5.5V7h1.5a.5.5 0 0 1 0 1H14v1.5a.5.5 0 0 1-1 0V8h-1.5a.5.5 0 0 1 0-1H13V5.5a.5.5 0 0 1 .5-.5"/>
                </svg>
                Cantidad total de cupos restantes: {{ totalAlumnosPermitidos - totalAlumnosInscritos }} cupos.
            </div>
            <div class="alert terminados">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-ban" viewBox="0 0 16 16">
                    <path d="M15 8a6.97 6.97 0 0 0-1.71-4.584l-9.874 9.875A7 7 0 0 0 15 8M2.71 12.584l9.874-9.875a7 7 0 0 0-9.874 9.874ZM16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0"/>
                </svg>
                Cantidad total de cursos terminados: {{ totalCursosTerminados }} cursos.
            </div>
            <div class="alert activos">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-bell-fill" viewBox="0 0 16 16">
                    <path d="M8 16a2 2 0 0 0 2-2H6a2 2 0 0 0 2 2m.995-14.901a1 1 0 1 0-1.99 0A5 5 0 0 0 3 6c0 1.098-.5 6-2 7h14c-1.5-1-2-5.902-2-7 0-2.42-1.72-4.44-4.005-4.901"/>
                </svg>
                Cantidad total de cursos activos: {{ totalCursosActivos }} cursos.
            </div>
            <div class="alert total">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-bell-fill" viewBox="0 0 16 16">
                    <path d="M8 16a2 2 0 0 0 2-2H6a2 2 0 0 0 2 2m.995-14.901a1 1 0 1 0-1.99 0A5 5 0 0 0 3 6c0 1.098-.5 6-2 7h14c-1.5-1-2-5.902-2-7 0-2.42-1.72-4.44-4.005-4.901"/>
                </svg>
                Cantidad total de cursos: {{ totalCursosActivos + totalCursosTerminados }} cursos.
            </div>
        </footer>
    </div>
</template>

<script>
import DetalleCurso from '@/components/DetalleCurso.vue';
import {mapGetters, mapState} from 'vuex';

export default {
    name: 'HomeView',
    data: function(){
        return{
            cabecera:{
                id: 0,
                nombre: 'NOMBRE',
                costo: 'COSTO',
                duracion: 'DURACIÓN',
                cupos: 'CUPOS',
                inscritos: 'INSCRITOS',
                completado: 'TERMINADO',
                fecha_registro: 'FECHA REGISTRO',
                descripcion: 'DESCRIPCIÓN',
                acciones: 'ACCIONES',
            },
            modalNuevo: true,
            mostrarModal: false,
            dialogNombre: '',
            dialogIMG: '',
            dialogCupos: '',
            dialogInscritos: '',
            dialogDuracion: '',
            dialogFecha: '',
            dialogCosto: '',
            dialogDescripcion: '',
        }
    },
    components: {
        DetalleCurso,
    },
    computed: {
        ...mapState({
            cursos: (state)=>state.cursos
        }),
        ...mapGetters([
            'totalAlumnosPermitidos',
            'totalAlumnosInscritos',
            'totalCuposRestantes',
            'totalCursosTerminados',
            'totalCursosActivos',
            'totalCursos',
        ])
    },
    methods:{
        agregarCurso(){
            this.modalNuevo = true;
            this.mostrarModal = true;
        },
        editarCurso(id){
            this.modalNuevo = false;
            console.log(id);
            this.mostrarModal = true;
        },
        ocultarModal(){
            this.mostrarModal = false;
        },
        limpiarFormulario(){
            this.dialogCosto = '';
            this.dialogCupos = '';
            this.dialogDescripcion = '';
            this.dialogDuracion = '';
            this.dialogFecha = '';
            this.dialogIMG = '';
            this.dialogInscritos = '';
            this.dialogNombre = '';
        },
    },
}
</script>

<style>
    dialog{
        border: 5px solid var(--bs-primary);
        border-radius: 20px;
        background-color: white;
        z-index: 1000;
    }
    section{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
    }
    footer{
        margin-top: 30px;
    }
    .alert{
        padding-block: 0.6rem;
        border-radius: 5px;
        border-width: 3px;
        text-align: left;
        font-weight: 700;
    }
    .permitidos{
        border-color: blueviolet;
        color: blueviolet;
    }
    .inscritos{
        border-color: dodgerblue;
        color: dodgerblue;
    }
    .restantes{
        border-color:rgb(228, 81, 81);
        color: rgb(228, 81, 81);
    }
    .terminados{
        border-color: darkorchid;
        color: darkorchid;
    }
    .activos{
        border-color: olive;
        color: olive;
    }
    .total{
        border-color: coral;
        color: coral;
    }
</style>