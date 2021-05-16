<template>
    <div class="user-profile">
        <div class="user-profile__avatar" :style="{ backgroundImage: `url('${avatar}')` }"></div>
        <div class="user-profile__container">
            <div class="user-profile__title" v-text="name"></div>
            <div class="user-profile__position" v-text="position"></div>
        </div>
    </div>
</template>

<script>
import './user-profile.scss';

export default {
    props: {
        avatar: {
            type: String,
            required: true
        },
        name: {
            type: String,
            default: null
        },
        position: {
            type: String,
            default: null
        }
    }
};
</script>
