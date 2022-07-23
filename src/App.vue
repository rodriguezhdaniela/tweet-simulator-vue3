<template>
 <Menu :openCloseForm="openCloseForm" :showForm="showForm"/>
 <tweetForm 
    :showForm="showForm" 
    :reloadTweets="reloadTweets" 
    :openCloseForm="openCloseForm"
  />
 <tweetList :tweets="tweets" :reloadTweets="reloadTweets"/>
</template>

<script>
import { ref } from "vue"
import Menu from "./components/Menu.vue"
import TweetForm from "./components/TweetForm.vue"
import TweetList from "./components/TweetList.vue"
import UseFormTweet from "./hooks/UseFormTweet"
import { getTweetsApi } from "./api/tweet"


export default {
  name: 'App',
  components: {
    Menu, 
    TweetForm, 
    TweetList
  },
  setup() {
    let tweets = ref(getTweetsApi().reverse())

    const reloadTweets = () => {
      tweets.value = getTweetsApi().reverse()
    }

    return {
      ...UseFormTweet(),
      tweets,
      reloadTweets,
    }
  }
  
}
</script>

<style>

</style>
