<template>

    <tr :class="this.$parent.isEdit(person.id)?'d-none': '' ">
        <td>{{ person.id }}</td>
        <td>{{ person.name }}</td>
        <td>{{ person.age }}</td>
        <td>{{ person.job }}</td>
        <td><a @click.prevent="changeEditPersonId(person.id, person.name, person.age, person.job)"
               class="btn btn-success">Edit</a></td>
        <td><a @click.prevent="deletePerson(person.id)" class="btn btn-danger">Delete</a></td>
    </tr>

</template>

<script>


export default {
    name: "ShowComponent",
    data() {
        return {
        }
    },

    mounted() {
    },
    props:[
        'person'
    ],
    methods: {

        changeEditPersonId(id, name, age, job) {
            this.$parent.editPersonId = id
            let editName = `edit_${id}`
            let fullEditName = this.$parent.$refs[editName][0]
            fullEditName.name = name
            fullEditName.age = age
            fullEditName.job = job
        },


        deletePerson(id) {
            axios.delete(`/api/people/${id}`).then(result => {
                this.$parent.getPeople()
            })
        },

    },

    computed: {}

}
</script>

<style scoped>

</style>
