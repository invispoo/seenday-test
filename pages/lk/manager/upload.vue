<template>
    <div>
        <main class="upload-page">
            <div class="upload-page__group">
                <Card class="upload-page__card"/>
                <div class="upload-page__info-group">
                    <div class="notice" data-color="light-purple" v-if="isInfoVisible">
                        Для того, чтобы просмотреть информацию о 
                        <span class="text-bold">выгрузке</span>, 
                        а также ее скачать, нажмите на требуемую выгрузку в столбце слева.
                    </div>
                    <div class="block upload-page__load" v-if="!isInfoVisible">
                        <span class="text-bold upload-page__load-header">Ссылка для скачивания архива Выгрузки (.zip):</span>
                        <br>
                        <a class="link upload-page__load-link">https://seenday.com/{{ downloadLink }}</a>
                        <span class="span-link" @click="copyLink">cкопировать ссылку</span>
                    </div>
                </div>
            </div>
            <div class="upload-page__upload-card-group">
                <UploadCard v-for="unload in fetchedData" :key="unload.id" :taskDate="unload.task_date"
                :statusText="unload.status_text" :event="unload.event" :size="unload.size" :id="unload.id"
                :status="unload.status" @click="getLink(unload.id)" class="upload-page__card"/>
            </div>
        </main>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import "~/assets/styles/components/notice/_notice.scss";
    import "~/assets/styles/components/notice/_data-color.scss";
    import "~/assets/styles/pages/upload/upload-page.scss";
    import "~/components/Card.vue";
    import "~/components/UploadCard.vue";

    const fetchedData = ref(null);
    const isInfoVisible = ref(true);
    const downloadLink = ref('');

    const { data } = useAPIFetch('https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get', {
        parseResponse: JSON.parse,
    });

    watch(data, () => {
        if (data) {
            fetchedData.value = data.value.response.data;
        }
    });

    function getLink(id) {
        const { data } = useAPIFetch(`https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_id=${id}`, {
            parseResponse: JSON.parse,
        });
        watch(data, () => {
            if (data) {
                downloadLink.value = data.value.response.data[0].download_link.match(/\d/g).join('');
                isInfoVisible.value = false;
            }
        });
    }

    function copyLink() {
        navigator.clipboard.writeText(`https://seenday.com/${downloadLink.value}`)
        .catch(err => console.log('При копировании произошла ошибка: ', err));
    }
</script>