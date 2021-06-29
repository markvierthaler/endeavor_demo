<template>
    <div>
       <CategoryHeader 
            v-bind:label="category.label" 
            v-bind:categoryUrl="category.categoryUrl" 
            />
       <div v-if="currentWidth >= breakpoint" class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <div v-if="index < listLimit && index % 2 == 0" class='row'>
                    <div class='column'>
                    <Item v-bind:item=item />
                    </div>
                    <div class='column' v-if='index+1 < category.items.length && index+1 < listLimit'>
                    <Item v-bind:item=category.items[index+1] />
                    </div>
                </div>    
            </div>
       </div>
       <div v-else class='main'>
            <div v-bind:key="item.id" v-for="item in category.items">
                <div v-if="index < listLimit" class='row'>
                <Item v-bind:item=item />
                </div>
            </div>
       </div>
    </div>
</template>

<script>
import Item from './Item';
import CategoryHeader from './CategoryHeader';

export default {
    name: "Category",
    components: {
        Item,CategoryHeader
    },
    props: {
        currentWidth: Number,
        breakpoint: Number,
        category: Object,
        listLimit: Number
    }
}
</script>

<style scoped>
    .main {
        position:relative;
        margin:10px;
        background-color:#ccc;
    }

    .row {

    }

    .column {
        float: left;
        width: 50%;
    }

     /* Clear floats after the columns */
    .row:after {
        content: "";
        display: table;
        clear: both;
    }

</style>
