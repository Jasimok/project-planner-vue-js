<template>
  <div class="home">
    <div v-if="projects.length" >
        <div v-for="(item, index) in projects" :key="index" >
            <SinglePage :project = "item" @delete = "handleDelete" @complete="handleComplete"/>
        </div>
    </div>
  </div>
</template>

<script>
import SinglePage from "../components/SinglePage.vue";
export default {
    name: 'HomeView',
    components: {
        SinglePage,
    },
  data() {
    return {
        projects: []
    }
  },
    mounted() {
        fetch('http://localhost:3000/projects')
            .then(res => res.json())
            .then(data => this.projects = data)
            .catch(err => console.log(err.message))
    },
  methods: {
    handleDelete(id) {
        this.projects =  this.projects.filter((project) => {
              return project.id !== id
        })
      },
      handleComplete(id) {
        let p =  this.projects.find(project => {
            return project.id === id
        })
        p.complete = !p.complete
    }
  },
}
</script>
