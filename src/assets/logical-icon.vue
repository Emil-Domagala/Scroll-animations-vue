<template>
    <svg id="mark" width="41" height="40" viewBox="0 0 41 40" fill="none" xmlns="http://www.w3.org/2000/svg"
        alt="Logical mark" :style='`transform: scale(${1 - scaleVal}) rotate(${rotateVal}turn);`'>
        <path
            d="M21.8791 14.7796C21.8136 14.8645 21.6777 14.8204 21.6746 14.7131L21.2606 0.000840082L18.9785 0L18.5458 14.983C18.5427 15.0902 18.4068 15.1343 18.3413 15.0493L9.20889 3.18924L7.50028 4.429L16.0995 17.0199C16.16 17.1084 16.076 17.2239 15.9732 17.1937L1.37349 12.909L0.774414 14.754L15.3565 19.9526C15.4575 19.9886 15.4575 20.1315 15.3565 20.1675L0.817088 25.3605L1.36426 27.0424L16.4321 22.6114C16.535 22.5811 16.619 22.6967 16.5585 22.7852L7.71538 35.717L9.0078 36.656L17.776 25.2846C17.8415 25.1996 17.9774 25.2438 17.9804 25.351L18.3932 39.9987L21.8164 40L22.2048 26.5678C22.2079 26.4605 22.3438 26.4164 22.4093 26.5014L30.5807 37.1125L33.1205 35.2696L25.338 23.8733C25.2775 23.7847 25.3615 23.6692 25.4644 23.6995L38.6718 27.5877L39.5729 24.821L26.2598 20.0611C26.1588 20.025 26.1589 19.8823 26.2598 19.8462L39.542 15.1021L38.7124 12.5521L24.8481 16.6292C24.7451 16.6594 24.6611 16.5438 24.7217 16.4553L32.8625 4.55086L30.8777 3.10883L21.8791 14.7796Z"
            fill="currentColor"></path>
    </svg>
</template>


<script>
export default {
    data() {
        return {
            scaleVal: 0,
            rotateVal: 0
        }
    },
    props: {
        scrollPercentage: {
            type: Number,
            requied: true
        }
    },
    watch: {
        scrollPercentage() {
            const scaleVal = (((Math.max((this.scrollPercentage), 15) - 15) * 1.1) / 100)
            this.scaleVal = Math.min(scaleVal, 0.25)
            const rotateVal = (((Math.max((this.scrollPercentage), 15) - 15) * 1.18) / 100)
            this.rotateVal = Math.min(rotateVal, 1)
        }
    }

}
</script>

<style scoped>
@import './_colors.css';


svg {
    height: 30px;
    color: var(--black-color);
}

@supports (mix-blend-mode: difference) {

    svg {
        color: var(--light-logo);
    }
}

@media(min-width: 420px) {
    svg {
        height: 40px;
    }
}
</style>