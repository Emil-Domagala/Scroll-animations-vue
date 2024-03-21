<template>
    <header id='header' :style='`transform: translateY(${-translateYVal}%); width:${widthVal}% `'>
        <Logical :scrollPercentage='scrollPercentage'></Logical>
        <LogicalIcon :scrollPercentage='scrollPercentage' />
    </header>
</template>

<script>
import LogicalIcon from '@/assets/logical-icon.vue';
import Logical from '@/assets/logical.vue';

export default {
    components: {
        LogicalIcon, Logical
    },
    data() {
        return {
            translateYVal: 0,
            widthVal: 100,
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
        pageWidth() {
            this.animations()
        },

        scrollPercentage() {
            this.animations()
        }
    },
    methods: {
        animations() {

            if (this.pageWidth >= 1200) {
                this.widthVal = 50
                const widthVal = 50 + ((Math.max((this.scrollPercentage), 15) - 15) * 1.1)
                this.widthVal = Math.min(widthVal, 100)
            } else {
                this.widthVal = 100
            }

            const translateYVal = ((Math.max((this.scrollPercentage), 15) - 15) * 1.1)
            this.translateYVal = Math.min(translateYVal, 25)
        }
    }
}
</script>


<style scoped lang='scss'>
#header {
    position: fixed;
    width: 100%;
    height: 40px;
    left: 0;
    top: 0;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-start;
    padding: 30px 20px;
    transform: translateY(0);
    z-index: 4;
    pointer-events: none;
    will-change: transform;
}

@supports (mix-blend-mode: difference) {
    #header {
        mix-blend-mode: difference;
    }
}

@media (min-width: 420px) {
    #header {
        padding: 60px;
    }
}

@media (min-width: 1200px) {
    #header {
        width: 50%;
        padding: 80px;
    }
}
</style>