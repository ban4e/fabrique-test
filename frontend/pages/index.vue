<template>
    <div class="grid-container mt-32">
        <BaseTabs :tabs="tabs" />
        <NuxtChild keep-alive />
    </div>
</template>

<script>
export default {
    data: () => ({
        tabs: [
            {
                title: 'Параметры',
                to: { name: 'index-params' }
            },
            {
                title: 'Вопросы',
                to: { name: 'index-questions' }
            },
            {
                title: 'Логика',
                to: { name: 'index-logic' }
            },
            {
                title: 'Условия',
                to: { name: 'index-condition' }
            },
            {
                title: 'Респонденты',
                to: { name: 'index' }
            }
        ]
    })
};
</script>
