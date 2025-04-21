<template>
    <Teleport to='body'>
        <Transition name='fade'>
            <div class="modal-wrapper" v-if='isVisible'>
                <div class="bgc"></div>
                <div class="modal">
                    <div class="wrapper__title">
                        <h3>{{ title }}</h3>
                    </div>
                    <div class="wrapper__message">
                        <p>{{ message }}</p>
                    </div>
                    <div class="wrapper__button"><button @click='close'>{{ button }}</button></div>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>

<script>
export default {

    emits: ['close'],

    props: {
        title: {
            type: String,
            required: true
        },
        message: {
            type: String,
            required: true
        },
        button: {
            type: String,
            required: true
        },
        isVisible: {
            type: Boolean,
            requied: true
        }

    }, methods: {
        close() {
            this.$emit('close');
            console.log('works in modal')
        },
    },
}
</script>

<style scoped lang='scss'>
.modal-wrapper {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
}

.bgc {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100vw;
    height: 100vh;
    background-color: #6e6e6ed2;
    z-index: 998;
}

.modal {
    padding: 0px;
    width: 80%;
    text-align: left;
    background: #FFFFFF;
    font-size: 14px;
    box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.25), 0px 15px 60px rgba(0, 0, 0, 0.15), 0px 5px 7px rgba(0, 0, 0, 0.05), 0px 4px 20px rgba(0, 0, 0, 0.04);
    border-radius: 10px;
    overflow: hidden;
    z-index: 1000;

    .wrapper__title,
    .wrapper__message,
    .wrapper__button {
        padding: 10px 20px 10px 20px;
        border-bottom: 1px solid #E6E9EA;
        text-align: center;
        font-size: 16px;

    }

    .wrapper__message {
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100px
    }

    h3 {
        font-weight: 600;
        font-size: 24px;
        letter-spacing: 1px;
        text-transform: uppercase;
    }

    button {
        display: block;
        width: 100%;
        color: #FFFFFF;
        background: #141616;
        border-radius: 8px;
        padding: 13px 20px;
        font-weight: 590;
    }
}

@media(min-width:800px) {
    .modal {
        width: 400px;
    }
}

.fade-enter-from,
.fade-leave-to {
    .bgc {
        opacity: 0;
    }

    .modal {
        transform: scale(0.8)
    }
}

.fade-enter-active,
.fade-leave-active {
    transition: all .4s ease-in-out, ;

    .bgc {
        transition: all .4s ease-in-out, ;
    }

    .modal {
        transition: transform .4s ease-in-out
    }
}
</style>