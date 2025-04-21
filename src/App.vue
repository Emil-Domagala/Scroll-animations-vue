<template>
  <Header :scrollPercentage='scrollPercentage' :pageWidth='pageWidth'/>
  <Screens :scrollPercentage='scrollPercentage' :scrollOffLastSection='scrollOffLastSection' :pageWidth='pageWidth'/>
  <Hero :scrollPercentage='scrollPercentage' :pageWidth='pageWidth'/>
  <Section1 />
  <Section2 />
  <Section3 />
  <Section4 />
  <SectionFinal :scrollOffLastSection='scrollOffLastSection' :pageWidth='pageWidth' />
  <Footer></Footer>
</template>

<script>
import Header from './components/header/header.vue';
import Screens from './components/screens/screens.vue';
import Hero from './components/sections/hero.vue';
import Section1 from './components/sections/section1.vue'
import Section2 from './components/sections/section2.vue'
import Section3 from './components/sections/section3.vue'
import Section4 from './components/sections/section4.vue'
import SectionFinal from './components/sections/sectionFinal.vue'
import Footer from './components/footer/footer.vue'

export default {
  components: {
    Header, Screens, Hero, Section1, Section2, Section3, Section4, SectionFinal, Footer
  },
  created() {
    window.addEventListener('scroll', this.scrollValue)
    window.addEventListener('resize', this.scrollValue)
    const htmlElement = document.documentElement
    this.pageWidth = htmlElement.clientWidth
  },
  unmounted() {
    window.removeEventListener('scroll', this.scrollValue)
    window.removeEventListener('resize', this.scrollValue)
  },
  data() {
    return {
      scrollPercentage: 0,
      scrollOffLastSection: 0,
      pageWidth: 0
    }
  },

  methods: {
    scrollValue() {
      const htmlElement = document.documentElement
      this.pageWidth = htmlElement.clientWidth

      const percentOfScrolledScreenHeight = htmlElement.scrollTop / htmlElement.clientHeight
      this.scrollPercentage = Math.min(percentOfScrolledScreenHeight * 100, 100)


      const percentOfScrolledFinalSection = 100 - (((htmlElement.scrollHeight - (htmlElement.clientHeight + htmlElement.scrollTop)) / htmlElement.clientHeight) * 100)
      this.scrollOffLastSection = Math.max(percentOfScrolledFinalSection, 0)
    }
  }
}

</script>

