<template>
    <div class="elements">
        <figure id='u1' :style='`transform:translateY(${u1Val}px)`'><img src="../../assets/deploy.png" alt="Logical App">
        </figure>
        <figure id='u2' :style='`transform:translateX(${-u2Val}px)`'><img src="../../assets/env-card.png" alt="Logical App">
        </figure>
        <figure id='u3' :style='`transform:translateX(${u3Val}px)`'><img src="../../assets/type.png" alt="Logical App">
        </figure>
        <figure id='u4' :style='`transform:translateY(${-u4Val}px)`'><img src="../../assets/modal.png" alt="Logical App">
        </figure>
    </div>
</template>

<script>

export default {
    data() {
        return {
            u1Val: 0,
            u2Val: 0,
            u3Val: 0,
            u4Val: 0

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
            this.u1Val = ((Math.max((this.scrollPercentage), 15) - 15) * 4.7)
            this.u2Val = ((Math.max((this.scrollPercentage), 15) - 15) * 1.2)
            this.u3Val = ((Math.max((this.scrollPercentage), 15) - 15) * 3.8)
            this.u4Val = ((Math.max((this.scrollPercentage), 15) - 15) * 9.4)
        }
    }
}

</script>

<style scoped lang='scss'>
.elements {
    z-index: 2;

    figure {
        position: absolute;
        padding: 0;
        margin: 0;
        opacity: 1;
        transform: translateX(0) translateY(0);
        z-index: 2;

        img {
            display: block;
            z-index: 2;

        }
    }

    #u1 {
        top: -90px;
        left: 15%;
        margin-left: -15%;
        width: 680px;
        height: 364px;
    }

    #u2 {
        top: 28%;
        left: -90px;
        width: 615px;
        height: 349px;
    }

    #u3 {
        right: -75px;
        bottom: -100px;
        width: 370px;
        height: 590px;
    }

    #u4 {
        bottom: -200px;
        width: 462px;
        height: 515px;
    }
}
</style>