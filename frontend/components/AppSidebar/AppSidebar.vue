<template>
    <div class="sidebar">
        <div class="sidebar__logo"></div>
        <div class="sidebar__menu">
            <div v-for="item in menuItems" :key="item.id" class="sidebar__menu-item">
                <NuxtLink :to="{ name: item.path }" class="sidebar__menu-link sidebar-link">
                    <BaseIcon :name="item.icon" :is-box="true" :width="40" class="sidebar-link__icon" />
                    <span class="sidebar-link__title" v-text="item.title"></span>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>

<script>
import './sidebar.scss';

export default {
    data: () => ({
        menuItems: [
            {
                id: 1,
                icon: 'list',
                title: 'Опросы',
                path: 'index'
            },
            {
                id: 2,
                icon: 'users',
                title: 'Пользователи',
                path: 'users'
            },
            {
                id: 3,
                icon: 'flag',
                title: 'Черные списки',
                path: 'banned'
            },
            {
                icon: 'phone',
                title: 'Колл-центр',
                path: 'call-center'
            }
        ]
    })
};
</script>
