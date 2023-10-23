<template>
    <div class="block">
        <div class="upload-card">
            <div>
                <div v-html="taskDate"></div>
                <div>
                    Статус задачи:
                    <span class="text-bold">{{ statusText }}</span>
                </div>
                <div>
                    ID выгрузки:
                    <span class="text-bold">{{ unloadId }}</span>
                </div>
                <div v-html="event"></div>
                <div>
                    Размер выгрузки:
                    <span class="text-bold">{{ size }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import "~/assets/styles/pages/upload/upload-card.scss"
    import { computed } from 'vue'

    const props = defineProps({
        taskDate: String,
        statusText: String,
        event: String,
        size: String,
        id: String,
    })

    const unloadId = computed(() => props.id - 2111)
</script>