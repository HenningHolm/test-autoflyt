<template>
    <div id="top-navigation">
        <h1 id=pageTitle>⇋ Autoflyt ⇋</h1>
    </div>
</template>

<script>
    export default {
        name:'TopNavigation'
       
    }
</script>

<style lang="css" scoped>

    #top-navigation{ 
        z-index: 100;
        position:absolute;
        top:0px;
        height: 60px;    
        width: 100vw;
        background: rgb(48, 52, 70);
        overflow: hidden;

        border: 1px solid gray;   
    }
    #pageTitle{
        text-align: center;
        font-size: 25px;
        color:burlywood;
        font-style: italic;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
    }
</style>