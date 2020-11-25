<template>
<div id ="right-sidebar">
    <div id="right-header">
        <button @click="toggle" id="rightmaxmin" style="width:30px; height:30px">-</button>
    </div> 
    <div class="optionCollection" id="drag-items" @dragstart="getDragElement">
        <div class="rightoption"><img src="../assets/Bucket.png" style= "position: relative;  top: 20px; left: 40px"/></div>
        <div class="rightoption"><img src="../assets/Bucket.png" style= "position: relative;  top: 20px; left: 40px"/></div>
        <div class="rightoption"><img src="../assets/Bucket.png" style= "position: relative;  top: 20px; left: 40px"/></div>
        <div class="rightoption"><img src="../assets/Bucket.png" style= "position: relative;  top: 20px; left: 40px"/></div>
        <div class="rightoption"></div>
        <div class="rightoption"></div>
        <div class="rightoption"></div>
        <div class="rightoption"></div>
    </div>
</div>
</template>

<script>

export default {
    name:'RightSidebar',
    data() {
        return {
            toggled: false,
            itemURL : '',

        }
    },

    methods: {

        getDragElement(e)
        {
            console.log("StartDrag");
            this.itemURL = e.target.src;
            console.log("draging: ", this.itemURL)
        },

        toggle()
        {
          
            if(this.toggled){  
                document.getElementById("right-sidebar").style.right = "0px";
                document.getElementById("right-header").style.right = "0px";
                document.getElementById("rightmaxmin").innerHTML = '-'
                this.toggled = false;
            }
            else{
                document.getElementById("right-sidebar").style.right = "-170px";
                document.getElementById("right-header").style.right = "-170px";
                document.getElementById("rightmaxmin").innerHTML = '+'
                this.toggled = true;
             }
        }
    }
}
</script>

<style lang="css" scoped>
    #right-sidebar{
        top: 0px;
        right: 0px;
        position: absolute;
        z-index: 100;
        height: 100vh;
        overflow-y: scroll;
    }
    #right-sidebar::-webkit-scrollbar {
    display: none;
    
}

.optionCollection
{
    top: 60px;
    position: relative;
}

#right-header{
    position: fixed;
    z-index: 110;
    height: 60px;
    width:  200px;
    top: 0px;
    right: 0px;
    border-bottom: 1px solid gray;
    border-top: 1px solid gray;
    border-left:1px solid gray;
    background-color: rgb(48, 52, 70);
}

    .rightoption {
    height: 140px;
    width:  200px;
    background-color: rgb(48, 52, 70);
    border-bottom: 1px solid gray;
    border-left:1px solid gray;
}

#rightmaxmin {
    float: left;
    position: relative;
}


</style>