<template>
    <div :key="componentKey" v-bind:style="{width: componentWidth + 'px'}">
       <CategoryHeader 
            v-bind:label="category.label" 
            v-bind:categoryUrl="category.categoryUrl" 
            />
        <!-- 3 Columns -->
        <div v-if="colCount==3" class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <!-- 3 Per Row -->
                <div v-if="index < listLimit && index % 3 == 0 && index+2 < category.items.length && index+2 < listLimit" class='row'>
                    <div class='column-3'>
                        <Item v-bind:item=item />
                    </div>
                    <div class='column-3'>
                        <Item v-bind:item=category.items[index+1] />
                    </div>    
                    <div  class='column-3'>
                        <Item v-bind:item=category.items[index+2] />
                    </div>
                </div>
                <!-- 2 Per Row -->
                <div v-else-if="index < listLimit && index % 3 == 0 && index+1 < category.items.length && index+1 < listLimit" class='row'>
                    <div class='column-2'>
                        <Item v-bind:item=item />
                    </div>
                    <div class='column-2'>
                        <Item v-bind:item=category.items[index+1] />
                    </div>    
                </div>
                <!-- 1 Per Row -->
                <div v-else-if="index < listLimit && index % 3 == 0 && index < category.items.length && index < listLimit" class='row'>
                    <div class='column-1'>
                        <Item v-bind:item=item />
                    </div>
                </div>
            </div>
        </div>
        <!-- 2 Columns -->
        <div v-else-if="colCount==2" class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <!-- 2 Per Row -->
                <div v-if="index < listLimit && index % 2 == 0 && index+1 < category.items.length && index+1 < listLimit" class='row'>
                    <div class='column-2'>
                        <Item v-bind:item=item />
                    </div>
                    <div class='column-2'>
                        <Item v-bind:item=category.items[index+1] />
                    </div>    
                </div>
                <!-- 1 Per Row -->
                <div v-else-if="index < listLimit && index % 2 == 0 && index < category.items.length && index < listLimit" class='row'>
                    <div class='column-1'>
                        <Item v-bind:item=item />
                    </div>
                </div>
            </div>
        </div>
        <!-- 1 Column -->
        <div v-else-if="colCount==1" class='main'>
            <div v-bind:key="item.id" v-for="(item, index) in category.items">
                <!-- 1 Per Row -->
                <div v-if="index < listLimit" class='row'>
                    <div class='column-1'>
                    <Item v-bind:item=item />
                    </div>
                </div>
            </div>
        </div>
        <div style='text-align:center;border:1px solid #bbb; padding:10px;margin:10px;'>
            Breakpoint - M: {{breakpointM}} | Breakpoint - L: {{breakpointL}} | <label :for="inputCurrentWidth">Component Width:</label><input :id="inputCurrentWidth"  v-model="userInputWidth" @keyup=onChangeWidthManually> | <label :for="inputListLimit">Display #:</label><input :id="inputListLimit" v-model="listLimit">
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
            componentWidth:0,
            userInputWidth:900,
            breakpointM:800,
            breakpointL:1200,
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
        setScreenSize() {
            this.componentWidth = document.body.clientWidth;
            this.updateCols(); 
            this.matchHeight();       
            this.componentKey++;
        },
        onResizeEventHandler: _.debounce(function(){
            this.setScreenSize();
        },5),
        onChangeWidthManually: _.debounce(function(){
            if(isNaN(this.userInputWidth) || this.userInputWidth<300) {    
                this.userInputWidth = 900;        
            }   
            this.componentWidth = this.userInputWidth;
            this.updateCols(); 
            this.matchHeight();      
            this.componentKey++;
        }, 1000),
        updateCols: _.debounce(function(){
            if(isNaN(this.componentWidth) || this.componentWidth<300) {    
                this.componentWidth = 900;        
            }   
            switch(true) {
                case this.componentWidth>=this.breakpointL:
                    this.colCount = 3
                    break;
                case this.componentWidth>=this.breakpointM:
                    this.colCount = 2
                    break;
                default:
                    this.colCount = 1
            }
            this.userInputWidth = this.componentWidth;
        }, 1000),
        
        matchHeight() {
            var rows = document.getElementsByClassName("row");   
            rows.forEach((row) => {
                var boxes =  row.getElementsByClassName("item_box");
                if(boxes.length>1) {
                    let boxMaxHeight = 0;
                    for(let i=0; i <boxes.length; i++){
                        boxMaxHeight = (parseInt(window.getComputedStyle(boxes[i],"").getPropertyValue("height")) > boxMaxHeight) ? parseInt(window.getComputedStyle(boxes[i],"").getPropertyValue("height")) : boxMaxHeight;
                    }    
                    for(let i=0; i <boxes.length; i++){
                        boxes[i].style.height = boxMaxHeight+"px";
                    }
                }
           })
        }
    },
    created() {
        window.addEventListener("resize", this.onResizeEventHandler);
    },
    mounted() {
        this.setScreenSize();
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

    .column-3 {
        overflow:hidden;
        float: left;
        width: 33%;
    }

     /* Clear floats after the columns */
    .row:after {
        content: "";
        display: table;
        clear: both;
    }

</style>
