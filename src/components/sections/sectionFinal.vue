<template>
    <section id='final'>
        <div data-show-img="img4" id='img4'></div>
        <div class="left">
            <h2>Get Early Access</h2>
            <p>Sign up now to secure your place in line, and get notified when we launch.</p>
        </div>
        <div class="right">
            <theForm :style='`transform: translateX(${-translateXVal}%) translateY(${-translateYVal}px)`'></theForm>
        </div>

         </section>
</template>

<script>

import theForm from './form/form.vue'

export default {
    data() {
        return {
            translateXVal: 0,
            translateYVal: 50,
        }
    },
    props: {
        scrollOffLastSection: {
            type: Number,
            requied: true
        },
        pageWidth: {
            type: Number,
            requied: true
        }
    },
    components: {
        theForm,
    },
    watch: {
        scrollOffLastSection() {
            this.animation()
        },
        pageWidth() {
            this.animation()
        }
    },
    methods: {
        animation() {
            this.translateXVal = 0;
            this.translateYVal = 50;
            if (this.pageWidth >= 1200) {
                this.translateXVal = (Math.max(this.scrollOffLastSection, 0) / 2)
                this.translateYVal = 0
            }
        }
    }
}
</script>

<style scoped lang='scss'>
@import '../../assets/_colors.css';

#final {
    display: block;
    height: auto;
    max-height: 100vh;
}

.left {
    padding-bottom: 140px;
    height: 100%;
}

.right {
    display: flex;
    height: 100%;

    background: #141616 url('../../assets/dark-bg.jpeg') no-repeat center center;
    background-size: cover;
    padding: 0;
}

@media (min-width:1200px) {
    #final {
        display: flex;
        flex-direction: row;
        height: 100vh;
        justify-content: space-between;
    }

    .left {
        padding: 80px;
        width: 50%;
    }

    .right {
        width: 35%;
    }
}
</style>
