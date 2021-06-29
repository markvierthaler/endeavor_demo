<template>
  <div id="app">
    <Category 
      v-bind:category=categories[0] 
      v-bind:currentWidth=currentWidth
      v-bind:breakpoint=breakpoint
      v-bind:listLimit=listLimit
      />
  </div>
</template>

<script>
import Category from './components/Category';

export default {
  name: 'app',
  components: {
    Category
  },
  data() {
    return {
      listLimit: "4",
      currentWidth:"800",
      breakpoint: "800",
      categories: [
        {
          label: "FEATURED BLOGS",
          categoryUrl: "/blog",
          items: [
            {
              id: 1,
              title: "Test Article 1",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/27/2021")
            },
            {
              id: 2,
              title: "Test Article 2",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/27/2021")
            },
            {
              id: 3,
              title: "Test Article 3",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/26/2021")
            },
            {
              id: 4,
              title: "Test Article 4",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/26/2021")
            },
            {
              id: 5,
              title: "Test Article 5",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/25/2021")
            },
            {
              id: 6,
              title: "Test Article 6",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/24/2021")
            },
            {
              id: 7,
              title: "Test Article 7",
              summary: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
              itemUrl: "https://www.endeavorbusinessmedia.com/",
              pubDate:  new Date("06/24/2021")
            }
            ]
        }  
      ]
    }
  }
}
</script>

<style>
  body {
    font-family: Arial, Arial, Helvetica, sans-serif;
  }
</style>
