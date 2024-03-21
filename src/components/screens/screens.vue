<template>
    <div class="screens"
        :style='`bottom:${-1 * bottomVal}%; transform: translateX(${-translateXVal}%)  scale(${scaleVal}) `'>
        <figure :class='whichImgShow === "img1" && "show"'>
            <img class='big' src="../../assets/big/index.png" alt="Logical App">
            <img class='mid' src="../../assets/mid/index_mid.png" alt="Logical App">
            <img class='small' src="../../assets/small/index_small.png" alt="Logical App">
        </figure>
        <figure :class='whichImgShow === "img2" && "show"'>
            <img class='big' src="../../assets/big/collections.png" alt="Logical App">
            <img class='mid' src="../../assets/mid/collections_mid.png" alt="Logical App">
            <img class='small' src="../../assets/small/collections_small.png" alt="Logical App">
        </figure>
        <figure :class='whichImgShow === "img3" && "show"'>
            <img class='big' src="../../assets/big/apis.png" alt="Logical App">
            <img class='mid' src="../../assets/mid/apis_mid.png" alt="Logical App">
            <img class='small' src="../../assets/small/apis_small.png" alt="Logical App">
        </figure>
        <figure :class='whichImgShow === "img4" && "img5" && "show"'>
            <img class='big' src="../../assets/big/functions.png" alt="Logical App">
            <img class='mid' src="../../assets/mid/functions_mid.png" alt="Logical App">
            <img class='small' src="../../assets/small/functions_small.png" alt="Logical App">
        </figure>
    </div>
</template>

<script>
export default {
    data() {
        return {
            bottomVal: 10,
            translateXVal: 0,
            scaleVal: 1,
            whichImgShow: 'img1',

        }
    },
    props: {
        scrollPercentage: {
            type: Number,
            requied: true
        },
        scrollOffLastSection: {
            type: Number,
            requied: true
        },
        pageWidth: {
            type: Number,
            requied: true
        }
    },
    watch: {
        pageWidth() {
            this.mainAnimation()
            this.bottomAnimation()
        },
        scrollPercentage() {
            this.mainAnimation()

            const observer = new IntersectionObserver(entries => {
                for (let i = entries.length - 1; i >= 0; i--) {
                    const entry = entries[i]
                    if (entry.isIntersecting) {
                        this.whichImgShow = entry.target.id
                    }
                }
            })
            document.querySelectorAll('[data-show-img]').forEach(section => { observer.observe(section) })
        },
        scrollOffLastSection() {
            this.bottomAnimation()
        }

    },
    methods: {
        mainAnimation() {

            const bottomVal = 10 - (this.scrollPercentage)
            this.bottomVal = Math.max(bottomVal, 0)
            this.scaleVal = 1
            this.translateXVal = 0

            if (this.pageWidth > 420) {
                const bottomVal = 20 - (this.scrollPercentage)
                this.bottomVal = Math.max(bottomVal, 0)
                this.scaleVal = 1
                this.translateXVal = 0
            }
            if (this.pageWidth > 800) {
                const bottomVal = 30 - (this.scrollPercentage)
                this.bottomVal = Math.max(bottomVal, 0)
                this.scaleVal = 1
                this.translateXVal = 0
            }


            if (this.pageWidth >= 1200) {
                const bottomVal = 10 - (this.scrollPercentage)
                this.bottomVal = Math.max(bottomVal, 0)
                const maxScalVal = 0.5 + (this.scrollPercentage / 50)
                this.scaleVal = Math.min(maxScalVal, 1)
                const translateXVal = 25 - (this.scrollPercentage)
                this.translateXVal = Math.max(translateXVal, 0)
            }
        },
        bottomAnimation(){
            this.bottomVal = (Math.max(this.scrollOffLastSection, 0) / 2.2)
        }
    }
}
</script>

<style scoped lang='scss'>
.screens {
    position: fixed;
    width: 100%;
    left: 0;
    right: 0;
    bottom: -10%;
    bottom: 0;
    padding: 0;
    margin: 0;
    line-height: 0;
    z-index: 2;
    transform: translateX(0) scale(1);
    transition: transform 0.1 ease-out;
    will-change: transform, bottom;

    figure {
        position: absolute;
        padding: 0;
        margin: 0;
        bottom: 0;
        left: 0;
        right: 0;
        transform: translateY(100%);
        transition: transform 0.35s ease-in-out;
        will-change: transform;

        img {
            width: 100%;
        }

        .big,
        .mid {
            display: none;
        }
    }

    .show {
        transform: translateY(0%) !important;
    }
}

@media(min-width: 800px) {
    .screens {
        figure {
            .small {
                display: none;
            }

            .mid {
                display: block;
            }
        }
    }
}

@media(min-width: 1200px) {
    .screens {
        figure {
            .mid {
                display: none;
            }

            .big {
                display: block;
            }
        }
    }
}
</style>