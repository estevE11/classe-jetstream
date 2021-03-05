<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Tasks
            </h2>
        </template>

        <div>
            <div class="max-w-7xl mx-auto py-10 sm:px-6 lg:px-8">
                <update-team-name-form :task="task" :permissions="permissions" />
                <table>
                    <tr>
                        <td>Team</td>
                        <td>Title</td>
                        <td>Description</td>
                    </tr>
                    <tr v-for="task in 10" :key="task" >
                        <td>task.team</td>
                        <td>task.title</td>
                        <td>task.description</td>
                    </tr>
                </table>
                
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'
    import JetSectionBorder from '@/Jetstream/SectionBorder'

    export default {
        props: [
            'task',
            'availableRoles',
            'permissions',
        ],

        components: {
            AppLayout,
            JetSectionBorder,
        },
    }
</script>

<style scoped>
    tr{
        background-color: red;
        }
</style>