<template>
    <div class="body__fallback">
        <div class="body__wrapper">
            <div class="body__sidebar">
                <AppSidebar />
            </div>
            <div class="body__main">
                <div class="body__header">
                    <AppHeader />
                </div>
                <div class="body__container">
                    <Nuxt />
                </div>
                <div class="body__footer"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    head() {
        return {
            bodyAttrs: {
                class: 'body'
            }
        };
    }
};
</script>
