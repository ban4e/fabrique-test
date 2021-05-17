<template>
    <form class="form-block" @submit.prevent="onSubmit">
        <div class="form-block__header">Добавить опрос</div>
        <div class="form-block__body">
            <RespondentBlock v-model="formData" />
        </div>
        <div class="form-block__footer">
            <BaseButton :is-loading="isRequest" @click.native.prevent="clearFormData"> Протестировать опрос (очистить все) </BaseButton>
            <BaseButton type="submit" theme="green" :is-loading="isLoading" class="ml-auto"> Далее </BaseButton>
        </div>
    </form>
</template>

<script>
export default {
    data: () => ({
        formData: [
            { base: '1', subLabel: 'Диапазон', subView: 'range', subItems: [{ valueFrom: null, valueTo: null }] },
            { base: '2', subLabel: 'Тип', subView: 'select', subItems: [{ value: '1' }, { value: null }] },
            { base: '3', subLabel: 'Статус', subView: 'select', subItems: [{ value: '1' }] }
        ],
        isLoading: false,
        isRequest: false
    }),
    methods: {
        async onSubmit() {
            try {
                this.isLoading = true;
                const result = await fetch('https://jsonplaceholder.typicode.com/posts', {
                    method: 'POST',
                    body: JSON.stringify({ ...this.formData }),
                    headers: {
                        'Content-type': 'application/json; charset=UTF-8'
                    }
                });
                const resultData = await result.json();
                this.$toast.success('Запрос отправлен. Результат в консоли');
                console.log(resultData);
            } catch (err) {
                console.error(err);
            } finally {
                this.isLoading = false;
            }
        },
        clearFormData() {
            this.formData = [];
        }
    }
};
</script>
