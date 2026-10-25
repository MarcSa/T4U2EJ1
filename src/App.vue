<script setup lang="ts">
import { ref } from 'vue';
import AlertComponent from '@/components/AlertComponent.vue';
import type { AlertProps } from '@/interfaces/alert-props.interface';
const alertSend = ref<AlertProps>({ message: '' });

const alertVisible = ref<boolean>(false);

const showAlert = (alert: AlertProps): void => {
    alertSend.value = alert;
    alertVisible.value = true;
};
</script>

<template>
    <header class="container pt-5">
        <div class="row" v-once>
            <div class="col-12 mb-4"><h1 class="text-center">Componente reutilizable</h1></div>
        </div>
    </header>
    <main class="container">
        <div class="row">
            <div class="col-12 justify-content-center d-flex mb-3">
                <AlertComponent
                    class="mx-1"
                    type="success"
                    message="Operación realizada correctamente"
                    @sendMessage="showAlert"
                    @close="alertVisible = false"
                />
                <AlertComponent
                    class="mx-1"
                    type="warning"
                    message="Mensaje de advertencia"
                    @sendMessage="showAlert"
                    @close="alertVisible = false"
                />
                <AlertComponent
                    class="mx-1"
                    type="error"
                    message="Se ha producido un error"
                    @sendMessage="showAlert"
                    @close="alertVisible = false"
                />
            </div>
        </div>
        <div class="row">
            <div class="col-12 justify-content-center d-flex">
                <div
                    v-if="alertVisible"
                    class="alert"
                    role="alert"
                    :class="`alert-${alertSend.type !== 'error' ? alertSend.type : 'danger'}`"
                >
                    <i class="bi bi-check-square-fill me-1" v-if="alertSend.type === 'success'"></i>
                    <i
                        class="bi bi-exclamation-triangle-fill me-1"
                        v-if="alertSend.type === 'warning'"
                    ></i>
                    <i class="bi bi-x-square-fill me-1" v-if="alertSend.type === 'error'"></i>
                    <i class="bi bi-info-square-fill me-1" v-if="alertSend.type === 'info'"></i>
                    {{ alertSend.message }}
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped></style>
