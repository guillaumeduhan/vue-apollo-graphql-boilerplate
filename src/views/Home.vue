<template lang="pug">
#Home
  header
    img.logo(src='https://myhappyagency.com/blog/wp-content/uploads/2019/12/vue-graphql-apollo.png')
    h1 {{ pjson.name }}
    p {{ pjson.description }}
    a(href="https://github.com/guillaumeduhan/vue-apollo-graphql-boilerplate", target="_blank") Github
</template>

<script>
import gql from 'graphql-tag'
import pjson from '../../package.json'

export default {
  name: 'Home',
  data() {
    return {
      pjson,
    }
  },
  apollo: {
    // Simple query that will update the 'hello' vue property
    hello: gql`query {
      hello
    }`,
  },
  methods: {
    async addTag() {
      // Call to the graphql mutation
      const result = await this.$apollo.mutate({
        // Query
        mutation: gql`mutation ($label: String!) {
          addTag(label: $label) {
            id
            label
          }
        }`,
        // Parameters
        variables: {
          label: this.newTag,
        },
      })
    }
  }
}
</script>

<style lang="scss">
#Home {
  .logo {
    max-width: 400px;
    margin: 30px 0;
    background: #C32424;
  }
}
</style>
