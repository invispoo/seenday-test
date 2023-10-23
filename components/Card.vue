<template>
    <div class="block">
        <div class="card">
            <div class="text-bold card__title">{{ title }}</div>
            <br>
            <div class="text-bold">{{ subtitle }}</div>
            <div class="card__text">{{ text }}</div>
        </div>
    </div>
</template>

<script setup>
    const title = 'Выгрузка';
    const subtitle = 'Выполняет работу:';
    const text = `- Собирает фотографии из заказов пользователей.\n- Выгружает по папкам.`
</script>
