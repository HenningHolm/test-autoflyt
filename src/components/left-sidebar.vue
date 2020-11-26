<template>
    <div id="left-sidebar">
        <div id="left-header">
            <button @click=" toggle" id="leftmaxmin" style="width:30px; height:30px">-</button>
        </div> 
        <div class="optionCollection">
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
            <div class="leftoption"></div>
        </div>
    </div>
</template>

<script>
export default {
    name:'LeftSidebar',


    methods: {

 toggle()
        {
            if(this.toggled){  
                document.getElementById("left-sidebar").style.left = "0px";
                document.getElementById("left-header").style.left = "0px";
                document.getElementById("leftmaxmin").innerHTML = '-'
                this.toggled = false;
            }
            else{
                document.getElementById("left-sidebar").style.left = "-170px";
                document.getElementById("left-header").style.left = "-170px";
                document.getElementById("leftmaxmin").innerHTML = '+'
                this.toggled = true;
             }
        }
    }
}
</script>

<style lang="css" scoped>
#left-sidebar {
    top: 0px;
    position : absolute; 
    z-index: 100;
    height: 100vh;
    overflow-y: scroll;



}
#left-sidebar::-webkit-scrollbar {
    display: none;
}

.optionCollection
{
    top: 60px;
    
    position: relative;
}

#left-header{
    position: fixed;
    z-index: 110;
    height: 60px;
    width:  200px;
    top: 0px;
    left: 0px;
    border-bottom: 1px solid gray;
    border-top: 1px solid gray;
    border-right:1px solid gray;
    background: rgb(45, 48, 58);
}

.leftoption {
    height: 140px;
    width:  200px;
   background: rgb(45, 48, 58);
    border-bottom: 1px solid gray;
    border-right:1px solid gray;
}

#leftmaxmin {
    float: right;
    position: relative;
    
}

</style>