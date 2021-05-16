<template>
    <form class="form-block" @submit.prevent="onSubmit">
        <div class="form-block__header">Добавить опрос</div>
        <div class="form-block__body">
            <RespondentBlock v-model="formData" />
        </div>
        <div class="form-block__footer">
            <BaseButton :is-loading="isRequest" @click.native.prevent="sendRequest"> Протестировать опрос (запрос) </BaseButton>
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
        onSubmit() {
            this.isLoading = true;
            setTimeout(() => {
                this.isLoading = false;
                this.$toast.show('Пустой обработчик отправки формы');
            }, 5000);
        },
        sendRequest() {
            try {
                this.isRequest = true;
                fetch('https://jsonplaceholder.typicode.com/posts')
                    .then(response => response.json())
                    .then(json => {
                        this.$toast.success('Запрос отправлен. Результат в консоли');
                        console.log(json);
                    });
            } catch (err) {
                console.error(err);
            } finally {
                this.isRequest = false;
            }
        }
    }
};
</script>
