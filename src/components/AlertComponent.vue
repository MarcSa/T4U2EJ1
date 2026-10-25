<script setup lang="ts">
import type { AlertProps } from '@/interfaces/alert-props.interface';

const props = withDefaults(defineProps<AlertProps>(), {
    type: 'error',
    message: 'Se ha producido un error',
    duration: 3000,
});

const emit = defineEmits<{
    (e: 'sendMessage', v: { message: string; type: AlertProps['type'] }): void;
    (e: 'close'): void;
}>();

const defineText = (type: AlertProps['type']): string => {
    if (type === 'success') return 'Correcto';
    if (type === 'warning') return 'Aviso';
    if (type === 'error') return 'Error';
    return 'Información';
};

const sendMessage = (): void => {
    emit('sendMessage', { message: props.message, type: props.type });
    setTimeout(() => {
        emit('close');
    }, props.duration);
};
</script>

<template>
    <button
        class="btn"
        :class="`btn-${props.type !== 'error' ? props.type : 'danger'}`"
        @click="sendMessage"
    >
        {{ defineText(props.type) }}
    </button>
</template>

<style scoped></style>
