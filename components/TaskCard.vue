<script>
export default {
    components: {
    },
    props: {
        task: {
            type: Object,
            default: () => ({})
        }
    },
    computed: {
    }
};
</script>

<template>
    <div class="bg-white shadow rounded px-3 pt-3 pb-5 border border-white">
        <div class="flex justify-between">
            <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">{{task.title}}</p>
        </div>
    </div>
</template>

<style scoped>

</style>