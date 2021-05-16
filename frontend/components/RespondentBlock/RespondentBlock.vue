<template>
    <div class="respondent">
        <div class="respondent__body">
            <div v-for="(condition, i) in localConditions" :key="i" class="respondent__condition">
                <div class="respondent__group respondent__group_main">
                    <div class="respondent__group-title" v-text="`Условие ${i + 1}`"></div>
                    <div class="respondent__group-prop">
                        <BaseSelect v-model="condition.base" :options="selectOptions" @change="onBaseConditionChange($event, i)" />
                    </div>
                </div>
                <div v-if="condition.base">
                    <div v-for="(subItem, subIndex) in condition.subItems" :key="subIndex" class="respondent__group mt-16">
                        <div class="respondent__group-title" v-text="`${subIndex > 0 ? 'Или ' : ''}${condition.subLabel} ${subIndex + 1}`"></div>
                        <div class="respondent__group-prop">
                            <template v-if="condition.subView === 'range'">
                                <span class="mr-4">От</span>
                                <BaseInput v-model="subItem.valueFrom" class="mr-16" />
                                <span class="mr-4">До</span>
                                <BaseInput v-model="subItem.valueTo" />
                            </template>
                            <template v-else-if="condition.subView === 'select'">
                                <BaseSelect v-model="subItem.value" :options="subOptions" />
                            </template>
                        </div>
                    </div>
                </div>
                <div class="respondent__condition-actions">
                    <BaseButton v-if="condition.base" theme="green" mod="_outline" @click.native.prevent="addSubItem(i)">{{
                        `Добавить ${condition.subLabel.toLowerCase()}`
                    }}</BaseButton>
                    <BaseButton class="respondent__condition-remove" theme="red" mod="_outline" @click.native.prevent="removeCondition(i)"> Удалить условие </BaseButton>
                </div>
            </div>
        </div>
        <div class="respondent__footer">
            <button type="button" class="respondent__add" @click.prevent="addCondition">
                <span class="respondent__add-title">+</span>
                <span class="respondent__add-description">
                    Нажмите, чтобы добавить новое условие выборки.<br />
                    Все условия связываются между собой логическим "И"
                </span>
            </button>
        </div>
    </div>
</template>

<script>
import './respondent.scss';

const CONDITION_OPTIONS = [
    { title: 'Выберите условие', value: null },
    { title: 'Возраст респондента', label: 'Диапазон', view: 'range', value: 1 },
    { title: 'Тип карты лояльности', label: 'Тип', view: 'select', value: 2 },
    { title: 'Статус карты лояльности', label: 'Статус', view: 'select', value: 3 }
];
const SUB_OPTIONS = [
    { title: 'Выберите значение', value: null },
    { title: 'Значение 1', value: 1 },
    { title: 'Значение 2', value: 2 },
    { title: 'Значение 3', value: 3 }
];

export default {
    model: {
        prop: 'conditions',
        event: 'change'
    },
    props: {
        conditions: {
            type: Array,
            required: true
        }
    },
    data: () => ({
        selectOptions: CONDITION_OPTIONS,
        subOptions: SUB_OPTIONS
    }),
    computed: {
        localConditions: {
            get() {
                return this.conditions;
            },
            set(value) {
                this.$emit('change', value);
            }
        }
    },
    methods: {
        /** Добавить условие */
        addCondition() {
            this.localConditions.push({
                base: null,
                subLabel: null,
                subView: null,
                subItems: null
            });
        },
        /**
         * Удалить условие
         * @param index - порядковый номер
         */
        removeCondition(index) {
            this.localConditions.splice(index, 1);
        },
        onBaseConditionChange(val, index) {
            const option = this.selectOptions.find(item => {
                return item.value === parseInt(val);
            });

            if (option && option.label && option.view) {
                this.localConditions.splice(
                    index,
                    1,
                    Object.assign(this.localConditions[index], {
                        subLabel: option.label,
                        subView: option.view,
                        subItems: [option.view === 'range' ? { valueFrom: null, valueTo: null } : { value: null }]
                    })
                );
            } else {
                this.localConditions.splice(
                    index,
                    1,
                    Object.assign({
                        base: null,
                        subLabel: null,
                        subView: null,
                        subItems: null
                    })
                );
            }
        },
        detectOptionsByBase(baseValue) {
            if (!baseValue) {
                return null;
            }

            return this.selectOptions.find(item => {
                return item.value === parseInt(baseValue);
            });
        },
        addSubItem(index) {
            const newSubItem = this.localConditions[index].subView === 'range' ? { valueFrom: null, valueTo: null } : { value: null };
            this.localConditions[index].subItems.push(newSubItem);
        }
    }
};
</script>
