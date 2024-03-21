<template>
    <section id="hero" :style='`transform: translateY(${section * -1}%)`'>
        <div class="left">
            <h1>Build Better Backends</h1>
            <p>The only platform that gives AI the ability to autonomously build web services.</p>
            <div class="bgc" :style='`opacity:${opacityVal}`'></div>
        </div>
        <div class="right">
            <div class="bgc" :style='`opacity:${opacityVal}`'></div>
            <Elements :scrollPercentage='scrollPercentage'></Elements>
        </div>
    </section>
</template>

<script>
import Elements from './elements.vue'
export default {
    components: {
        Elements
    },
    data() {
        return {
            section: 0,
            opacityVal: 1
        }
    },
    props: {
        scrollPercentage: {
            type: Number,
            requied: true
        },
        pageWidth: {
            type: Number,
            requied: true
        }
    },
    watch: {
        scrollPercentage() {
            this.opacityVal = 1 - (Math.max((this.scrollPercentage), 0) / 21)
            this.section = 0
            if (this.pageWidth >= 1200) {
                this.section = ((Math.max((this.scrollPercentage), 15) - 15) * 100 / 85)
            }
        }
    }
}
</script>

<style scoped lang='scss'>
@import '../../assets/_colors.css';


#hero {
    position: relative;
    top: 0;
    z-index: 1;

}

.bgc {
    position: absolute;
    z-index: -1;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    opacity: 1;
}

.left {
    .bgc {
        background-color: var(--left-hero-color);
    }
}

.right {
    position: relative;
    width: 50%;
    height: 100%;

    .bgc {
        background-color: var(--right-hero-color);
    }
}

@media (min-width: 420px) {
    .left {
        padding: 80px;
    }
}

@media (min-width:1200px) {

    #hero {
        position: fixed;
    }

    .left {
        width: 50%;
        // text-align: left;
        // align-items: flex-start;
    }
}
</style>