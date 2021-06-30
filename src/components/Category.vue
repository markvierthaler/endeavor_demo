<template>
    <div :key="colCount" v-bind:style="{width: componentWidth + 'px'}">
       <CategoryHeader 
            v-bind:label="category.label" 
            v-bind:categoryUrl="category.categoryUrl" 
            />
        <div v-if="colCount==2" class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <div v-if="index < listLimit && index % 2 == 0" class='row'>
                    <div class='column-2'>
                    <Item v-bind:item=item />
                    </div>
                    <div class='column-2' v-if='index+1 < category.items.length && index+1 < listLimit'>
                    <Item v-bind:item=category.items[index+1] />
                    </div>
                </div>    
            </div>
        </div>
        <div v-else class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <div v-if="index < listLimit" class='row'>
                    <div class='column-1'>
                    <Item v-bind:item=item />
                    </div>
                </div>
            </div>
        </div>
        <div style='text-align:center;border:1px solid #bbb; padding:10px;margin:10px;'>
            Breakpoint: {{breakpoint}} | <label :for="inputCurrentWidth">Component Width:</label><input :id="inputCurrentWidth"  v-model="userInputWidth" @keyup=updateCols> | <label :for="inputListLimit">Display #:</label><input :id="inputListLimit" v-model="listLimit">
        </div>
    </div>
    
</template>

<script>
import Item from './Item';
import CategoryHeader from './CategoryHeader';
import _ from "lodash";

export default {
    name: "Category",
    data() {
        return {
            listLimit: 4,
            colCount:2,
            componentWidth:900,
            userInputWidth:900,
            breakpoint:800,
            componentKey:0
        };
    },
    components: {
        Item,
        CategoryHeader
    },
    props: {
        category: Object
    },
    methods: {
        updateCols: _.debounce(function(){
            if(isNaN(this.userInputWidth) || this.userInputWidth<300) {    
                this.userInputWidth = 900;        
            }   
            this.userInputWidth >= this.breakpoint ? this.colCount = 2 : this.colCount = 1;
            this.componentWidth = this.userInputWidth;
        }, 1000),
        matchHeight() {
            var rows = document.getElementsByClassName("row");   
            rows.forEach((row) => {
                var boxes =  row.getElementsByClassName("item_box");
                if(boxes.length>1) {
                    if(boxes[0].clientHeight > boxes[1].clientHeight) {
                        boxes[1].style.height  = window.getComputedStyle(boxes[0],"").getPropertyValue("height")
                    } else if(boxes[0].clientHeight<boxes[1].clientHeight) {
                        boxes[0].style.height  = window.getComputedStyle(boxes[1],"").getPropertyValue("height")
                    }
                }
           })
        }
    },  
    mounted() {
        this.matchHeight();  
    },      
    updated() {
        this.matchHeight();       
    }    
}
</script>

<style scoped>

    input {
        width:30px;
    }

    .main {
        position:relative;
        overflow:hidden;
        margin:10px;
        background-color:#ccc;
    }

    .row {
        position:relative;
        overflow:hidden;
    }

    .column-1 {
        overflow:hidden;
        width: 66%;
        margin-left:auto;
        margin-right:auto;
        height:100%;
    }

    .column-2 {
        overflow:hidden;
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
