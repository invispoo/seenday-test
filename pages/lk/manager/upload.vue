<template>
    <div>
        <main class="upload-page">
            <div class="upload-page__cards-group">
                <Card />
                <UploadCard v-for="unload in fetchedData" :key="unload.id" :taskDate="unload.task_date"
                    :statusText="unload.status_text" :event="unload.event" :size="unload.size" :id="unload.id" @click="isInfoVisible=false"/>
            </div>
            <div class="upload-page__info">
                <div class="notice" data-color="light-purple" v-if="isInfoVisible">
                    Для того, чтобы просмотреть информацию о <span class="text-bold">выгрузке</span>,
                    а также ее скачать, нажмите на требуемую выгрузку в столбце слева.
                </div>
                <div class="block" v-if="!isInfoVisible">
                    <span class="text-bold">Ссылка для скачивания архива Выгрузки (.zip):</span>
                    <br>
                    <a class="link"></a>
                    <span class="span-link">cкопировать ссылку</span>
                </div>
            </div>
        </main>
    </div>
</template>

<script setup >
import { ref, onBeforeMount } from 'vue';
import "~/assets/styles/components/notice/_notice.scss";
import "~/assets/styles/components/notice/_data-color.scss";
import "~/assets/styles/pages/upload/upload-page.scss";
import "~/components/Card.vue";
import "~/components/UploadCard.vue";

const fetchedData = ref(null);
const isInfoVisible = ref(true);
onBeforeMount(() => {
    const { data } = useAPIFetch('https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get', {
        parseResponse: JSON.parse,
    });

    watch(data, () => {
        if (data) {
            fetchedData.value = data.value.response.data;
        }
    });
})


</script>