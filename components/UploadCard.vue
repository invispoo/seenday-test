<template>
    <div class="block">
        <div>
            <div class="upload-page__upload-card" :class="status === 'green' ?  'upload-page__upload-card_success' :  'upload-page__upload-card_danger'">
                <div v-html="taskDate"/>
                <div>
                    Статус задачи:
                    <span class="text-bold">{{ statusText }}</span>
                </div>
                <div>
                    ID выгрузки:
                    <span class="text-bold">{{ unloadId }}</span>
                </div>
                <div v-html="event"/>
                <div>
                    Размер выгрузки:
                    <span class="text-bold">{{ size }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import "~/assets/styles/pages/upload/upload-page.scss"
    import { computed } from 'vue'

    const props = defineProps({
        taskDate: String,
        statusText: String,
        event: String,
        size: String,
        id: String,
        status: String
    })

    const unloadId = computed(() => props.id - 2111)
</script>