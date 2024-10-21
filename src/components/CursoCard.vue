<template>
    <div class="curso card">
        <img :src="curso.img" alt="">
        <h4>{{ curso.nombre }}</h4>
        <div class="info">
            <span>Información</span>
            <div class="separator">
                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-cart-check-fill" viewBox="0 0 16 16">
                    <path d="M.5 1a.5.5 0 0 0 0 1h1.11l.401 1.607 1.498 7.985A.5.5 0 0 0 4 12h1a2 2 0 1 0 0 4 2 2 0 0 0 0-4h7a2 2 0 1 0 0 4 2 2 0 0 0 0-4h1a.5.5 0 0 0 .491-.408l1.5-8A.5.5 0 0 0 14.5 3H2.89l-.405-1.621A.5.5 0 0 0 2 1zM6 14a1 1 0 1 1-2 0 1 1 0 0 1 2 0m7 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0m-1.646-7.646-3 3a.5.5 0 0 1-.708 0l-1.5-1.5a.5.5 0 1 1 .708-.708L8 8.293l2.646-2.647a.5.5 0 0 1 .708.708"/>
                </svg>
                <div class="textInfo">
                    <span>Costo: {{ curso.costo }}</span>
                    <span>Duración: {{ curso.duracion }}</span>
                </div>
            </div>
            <div class="separator">
                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-person-fill-check" viewBox="0 0 16 16">
                    <path d="M12.5 16a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7m1.679-4.493-1.335 2.226a.75.75 0 0 1-1.174.144l-.774-.773a.5.5 0 0 1 .708-.708l.547.548 1.17-1.951a.5.5 0 1 1 .858.514M11 5a3 3 0 1 1-6 0 3 3 0 0 1 6 0"/>
                    <path d="M2 13c0 1 1 1 1 1h5.256A4.5 4.5 0 0 1 8 12.5a4.5 4.5 0 0 1 1.544-3.393Q8.844 9.002 8 9c-5 0-6 3-6 4"/>
                </svg>
                <div class="textInfo">
                    <span>Cupos: {{ curso.cupos }}</span>
                    <span>Completado: {{ completado }}</span>
                </div>
            </div>
            <div class="separator">
                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-calendar2-check-fill" viewBox="0 0 16 16">
                    <path d="M3.5 0a.5.5 0 0 1 .5.5V1h8V.5a.5.5 0 0 1 1 0V1h1a2 2 0 0 1 2 2v11a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V3a2 2 0 0 1 2-2h1V.5a.5.5 0 0 1 .5-.5m9.954 3H2.545c-.3 0-.545.224-.545.5v1c0 .276.244.5.545.5h10.91c.3 0 .545-.224.545-.5v-1c0-.276-.244-.5-.546-.5m-2.6 5.854a.5.5 0 0 0-.708-.708L7.5 10.793 6.354 9.646a.5.5 0 1 0-.708.708l1.5 1.5a.5.5 0 0 0 .708 0z"/>
                </svg>
                <div class="textInfo">
                    <span>Fecha de Registro:</span>
                    <span>{{ curso.fecha_registro }}</span>
                </div>
            </div>
            <div class="separator">
                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-info-square-fill" viewBox="0 0 16 16">
                    <path d="M0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2zm8.93 4.588-2.29.287-.082.38.45.083c.294.07.352.176.288.469l-.738 3.468c-.194.897.105 1.319.808 1.319.545 0 1.178-.252 1.465-.598l.088-.416c-.2.176-.492.246-.686.246-.275 0-.375-.193-.304-.533zM8 5.5a1 1 0 1 0 0-2 1 1 0 0 0 0 2"/>
                </svg>
                <div class="textInfo">
                    <span>Descripción:</span>
                    <span>{{ curso.descripcion }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: 'CursoCard',
    props: {
        curso:{
            type:Object,
            required: true,
        }
    },
    data: function(){
        return{}
    },
    computed: {
        completado(){
            if(this.curso.completado){
                return 'Si'
            }
            else{
                return 'No'
            }
        }
    },
    //methods: {},
    //watch: {},
    //components: {},
    //mixins: [],
    //filters: {},
    //-- LifeCycle Methods
    //-- End LifeCycle Methods
}
</script>

<style scoped>

    .curso{
        width: 400px;
        padding: 20px;
        margin-bottom: 40px;
        margin-inline: 10px;
    }
    img{
        height: 250px;
        width: fit-content;
        margin-bottom: 30px;
        align-self: center;
    }
    li{
        display: flex;
        flex-direction: row;
    }
    .info{
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    .separator{
        margin-inline-start: 5em;
        margin-block-start: 1.5em;
        gap: 1em;
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
    }
    .textInfo{
        margin-inline-start: 1rem;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        max-width: 180px;
    }
    .textInfo span{
        text-align: start;
    }
</style>