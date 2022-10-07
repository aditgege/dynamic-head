<template>
  <article>
    <SocialHead
      :title="title"
      :description="description"
      :image="image"
    />
    <h1>{{ mountain.title }}</h1>
    <section>
      <img :src="mountain.image" :alt="mountain.title" />
      <p>{{ mountain.description }}</p>
    </section>
    <button @click="goBack">Back</button>
  </article>
</template>
<script>
import SocialHead from '~/components/SocialHead.vue'
export default {
  components: {
    SocialHead
  },
  data() {
    return {
      mountain: null
    }
  },

  async fetch() {
    const { slug } = this.$route.params
    const response = await fetch(
      `https://api.nuxtjs.dev/mountains/${slug}`
    )
    this.mountain = await response.json()
  },
  // async asyncData({ params }) {
  //   const mountain = await fetch(
  //     `https://api.nuxtjs.dev/mountains/${params.slug}`
  //   ).then((res) => res.json())
  //   return { mountain }
  // },
  methods: {
    goBack() {
      return this.$router.go(-1)
    }
  },

  computed: {
    title() {
      return this.mountain.title
    },
    description() {
      return this.mountain.description
    },
    image() {
      return this.mountain.image
    }
  },
  head() {
    return {
      title: this.title,
      link: [
        {
          hid: 'canonical',
          rel: 'canonical',
          href: `https://nuxtjs.org/mountains/${this.$route.params.slug}`
        }
      ]
    }
  }
}
</script>
<style scoped>
article {
  max-width: 600px;
  margin: 0 auto;
}
img {
  height: 200px;
}
p {
  text-align: left;
}
</style>
