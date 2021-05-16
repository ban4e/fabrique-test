<template>
    <div class="tabs">
        <div class="tabs__container">
            <div v-for="(tab, i) in tabs" :key="i" class="tabs__item">
                <NuxtLink :to="tab.to" class="tabs__link">{{ tab.title }}</NuxtLink>
            </div>
        </div>
    </div>
</template>

<script>
import './tabs.scss';

export default {
    props: {
        tabs: {
            type: Array,
            required: true
        }
    }
};
</script>
