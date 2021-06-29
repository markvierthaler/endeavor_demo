<template>
    <div class='item_box'>
        <span class="fa-stack fa-2x" style='margin-top:-40px;margin-left:-60px;'>
        <i class="fas fa-circle fa-stack-2x"></i>
        <div class="fa-stack-1x" style="color:white; font-size:12pt;line-height:20px;margin-top:12px;text-align:center;">{{parseMonth(item.pubDate)}}</div>
        <div class="fa-stack-1x" style="color:white; font-size:12pt;line-height:20px;margin-top:30px;text-align:center;">{{parseDay(item.pubDate)}}</div>
        </span>
        <div>
        <a v-bind:href="item.itemUrl" class="item_title">{{item.title}}</a><br/>
        {{item.summary}}
        </div>  
    </div>
</template>

<script>

export default {
    name: "Item",
    components: {

    },
    props: {
        item: Object
    },
    methods: {
        parseMonth(value) {
            const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",  "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
            if(value) {
                return monthNames[value.getMonth()];
            }
        },
        parseDay(value) {
            if(value) {
                return value.getDate();
            }
        }
    }
}
</script>

<style scoped>
    .item_box {
        position:relative;
        border:1px solid #000;
        background: #fff;
        padding:20px 20px;
        margin:40px;
    }
    .item_title {
        font-size:18pt;
        font-weight:bold;
        color:#000;
        text-decoration: none;
    }
    .item_title:hover {
        text-decoration:underline;
    }    
</style>
