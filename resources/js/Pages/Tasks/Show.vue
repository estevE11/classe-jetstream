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
                Buenas
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
