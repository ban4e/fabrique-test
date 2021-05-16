<template>
    <div class="selector">
        <select class="selector__select" v-bind="$attrs" @change="onChange">
            <option v-for="(optionData, i) in options" :key="i" class="selector__option" :value="optionData.value">
                {{ optionData.title }}
            </option>
        </select>
        <div class="selector__indicator-wrapper">
            <BaseIcon name="angle-down" class="selector__indicator" :is-box="true" />
        </div>
    </div>
</template>

<script>
import './select.scss';

export default {
    inheritAttrs: false,
    model: {
        prop: 'value',
        event: 'change'
    },
    props: {
        options: {
            type: Array,
            reqiured: true,
            default: null
        },
        value: {
            type: [Number, String],
            reqiured: true,
            default: null
        }
    },
    computed: {
        localValue: {
            get() {
                return this.value;
            },
            set(val) {
                this.$emit('change', val);
            }
        }
    },
    methods: {
        onChange(e) {
            const { value } = e.target;
            this.localValue = value;
        }
    }
};
</script>
