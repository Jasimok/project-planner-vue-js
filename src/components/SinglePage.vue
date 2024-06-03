<template>
    <div class="projects" :class="{complete : project.complete}">
        <div class="pro-title">
            <h2 @click="showdetails = !showdetails" >{{ project.title }}</h2>
            <div class="icons">
                <span @click="handleCheck" class="material-symbols-outlined">check</span>
                <router-link :to="{name:'EditProject',params:{ id: project.id }}"><span class="material-symbols-outlined">edit</span></router-link>
                <span @click="handleDelete" class="material-symbols-outlined">delete</span>
            </div>
        </div>
        <div v-if="showdetails" class="pro-desc">
            <p>{{ project.details }}</p>
        </div>
    </div>
</template>

<script>
    export default {
    props: ["project"],
        data() {
            return {
                showdetails: false,
                uri:'http://localhost:3000/projects/'+ this.project.id
            }
    },
        methods: {
            handleDelete() {
                fetch(this.uri, { method: 'DELETE' })
                    .then(() => this.$emit('delete', this.project.id))
                    .catch(err => console.log(err))
            },
            handleCheck() {
                fetch(this.uri, {
                    method: 'PATCH',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ complete: !this.project.complete })
                }).then(() => this.$emit('complete', this.project.id))
                .catch(err => console.log(err) )
            }
        },
    }
</script>

<style scoped>
.projects {
    margin: 20px auto;
    background-color: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;
}
.pro-title h2 {
    cursor: pointer;
}
.pro-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
span.material-symbols-outlined {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}

span.material-symbols-outlined:hover {
    color: #777;
}
.projects.complete {
    border-left: 4px solid #00ce89;
}
</style>