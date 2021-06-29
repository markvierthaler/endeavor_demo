<template>
    <div class='category_header'>
        <span class="fa-stack fa-2x" style='margin-top:-30px;'>
            <i class="fas fa-circle fa-stack-2x"></i>
            <i class="fas fa-rss fa-stack-1x fa-inverse"></i>
        </span>
        <a v-bind:href="categoryUrl">{{label}}</a>
    </div>
</template>

<script>
export default {
    name: "CategoryHeader",
    props: {
        label: String,
        categoryUrl: String
    }
}
</script>

<style scoped>
    .category_header {
        position:relative;
        margin:30px 10px 10px 10px;
        height:45px;
        background-color:#ddd;
    }

    .category_header a {
        font-weight:bold;
        font-size:15pt;
        line-height: 50px;
        color:#000;
        text-decoration:none;   
    }

    .category_header a:hover {
        text-decoration:underline;
    }
</style>