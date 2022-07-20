<script>
export default {
    props: {
        carouselData: Array
    },
    data: () => ({
        index: 0,
        dialogHeight: 0
    }),
    methods: {
        next: function () {
            this.index = (this.index + 1) % this.carouselData.length;
        },
        updateHeight: function () {
            const newDialogHeight = document.querySelector(".modal__dialog.modal__dialog--sentinel").getBoundingClientRect().height;
            console.log(`New dialog height: ${newDialogHeight}px`);
            this.dialogHeight = newDialogHeight;
        }
    },
    mounted: function () {
        this.updateHeight();
    }
}
</script>

<template>
    <div class="modal">

        <!-- Fake background -->
        <div class="modal__fake-bg" :style="{ height: dialogHeight == 0 ? `auto` : `${dialogHeight}px` }" />

        <!-- Actual dialog -->
        <article class="modal__dialog modal__dialog--actual">

            <!-- Title -->
            <transition name="dialog-title--actual" mode="out-in">
                <template v-for="(data, i) in carouselData">
                    <h1 :key="i" v-if="i == index" class="modal__dialog__heading">
                        {{ data.title }}
                    </h1>
                </template>
            </transition>

            <!-- Description -->
            <transition name="dialog-desc--actual" mode="out-in">
                <template v-for="(data, i) in carouselData">
                    <p :key="i" v-if="i == index" class="modal__dialog__desc">
                        {{ data.description }}
                    </p>
                </template>
            </transition>
        </article>

        <!-- Button to go forward -->
        <button class="modal__button" @click="next">Next</button>

        <!-- Sentinel dialog -->
        <article class="modal__dialog modal__dialog--sentinel">
            <!-- Title -->
            <transition name="dialog-title--sentinel" mode="out-in" @after-enter="updateHeight">
                <template v-for="(data, i) in carouselData">
                    <h1 :key="i" v-if="i == index" class="modal__dialog__heading">
                        {{ data.title }}
                    </h1>
                </template>
            </transition>

            <!-- Description -->
            <transition name="dialog-desc--sentinel" mode="out-in" @after-enter="updateHeight">
                <template v-for="(data, i) in carouselData">
                    <p :key="i" v-if="i == index" class="modal__dialog__desc">
                        {{ data.description }}
                    </p>
                </template>
            </transition>
        </article>
    </div>
</template>

<style scoped>
.modal {
    width: 100%;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
}

.modal__dialog {
    width: 100%;
    max-width: 320px;
    padding: 1rem;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
}

.modal__fake-bg {
    width: 100%;
    max-width: 320px;
    border-radius: 8px;
    box-shadow: 2px 3px 11px -8px #000000;
    background-color: #fff;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    transition: height 1s ease-out;
}

.modal__dialog--actual {
    z-index: 2;
}

.modal__dialog--sentinel {
    z-index: 1;
    opacity: 0;
    user-select: none;
    touch-action: none;
    pointer-events: none;
}

.modal__button {
    background-color: rgb(153, 87, 195);
    color: #ffffff;
    padding: 0.75rem 1.65rem;
    border-radius: 4px;
    margin: 2rem 0 0 auto;
    position: fixed;
    bottom: 5%;
    left: 50%;
    transform: translateX(-50%);
}

/* Animations */
.dialog-title--actual-enter,
.dialog-desc--actual-enter {
    opacity: 0;
    transform: translateX(32px);
}

.dialog-title--actual-enter-to,
.dialog-title--actual-leave,
.dialog-desc--actual-enter-to,
.dialog-desc--actual-leave {
    opacity: 1;
    transform: translate(0, 0);
}

.dialog-title--actual-leave-to,
.dialog-desc--actual-leave-to {
    opacity: 0;
    transform: translateX(-32px);
}

.dialog-title--actual-enter-active,
.dialog-title--actual-leave-active,
.dialog-desc--actual-enter-active,
.dialog-desc--actual-leave-active {
    transition: all 1s ease-out;
}
</style>