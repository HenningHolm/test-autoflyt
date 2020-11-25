<template>
  <div style="">
    <v-stage
      ref="stage"
      id="container"
      :config="stageConfig"
      @wheel="resize"
    style="overflow: hidden">
     <v-layer ref="layer2" id="lay2"
      @dragstart="handleDragstart"
      @dragend="handleDragend">
        <!-- <v-rect
          :config="{
            x: -1500,
            y: -1500,
            height: 4000,
            width: 6000, 
            fillPatternImage: image,
            opacity: 1,
            shadowColor: 'black',
            shadowBlur: 10,
            shadowOpacity: 0.6,
          }"
        >   </v-rect> -->
             <v-image :config="{
            image: image
          }"/>
      
      
       
      </v-layer>
      <v-layer ref="layer" id="lay"
      @dragstart="handleDragstart"
      @dragend="handleDragend">
        <v-rect
          v-for="item in list"
          :key="item.id"
          :config="{
            x: item.x,
            y: item.y,
            rotation: item.rotation,
            id: item.id,
            height: 60,
            width: 100, 
            fill: item.fill,
            opacity: 0.8,
            draggable: true,
            shadowColor: 'black',
            shadowBlur: 10,
            shadowOpacity: 0.6,
          }"
        ></v-rect>
      </v-layer>

    </v-stage>
  </div>
</template>


<script>

import Konva from 'konva';
const width = window.innerWidth;
const height = window.innerHeight;

export default {
    name: 'MainCanvas',
  data() {
    return {
      list: [],
      mainStage : undefined,
      mainLayer: undefined,
      dragItemId: "",
      image: null,
      itemUrl : null, //rename
      stageConfig: {
        container: 'container',
        width: 4000,
        height: 4000,
        draggable: true,
      }, 
      retotus: undefined
    };
  },

  methods: {
    handleDragstart(e) {
      // save drag element:
      this.dragItemId = e.target.id();
      console.log(this.dragItemId)

      // move current element to the top
      // the highter the index, the higher z-value
      const item = this.list.find(i => i.id === this.dragItemId);
      const index = this.list.indexOf(item);
      this.list.splice(index, 1);
      this.list.push(item); 
 
     
    },
    loadImage(){
     
    }
    ,
    resize(e){
    var stage = e.target.getStage(); 
    var stageXScale= stage.scaleX()- e.evt.deltaY/2000;
    var stageYScale= stage.scaleY()- e.evt.deltaY/2000;
    
    stage.scale({ x: stageXScale, y:stageYScale })
    stage.batchDraw();
  //  console.log("updateValue");
   
    //console.log("main : ", this.mainStage)

    // let image = new Image();
    // image.src = "../assets/gridElement.png";
    //console.log("stage", this.$refs.stage.getNode())
    },

    handleDragend() {
      this.dragItemId = null;
    },


  },
  mounted() {
    for (let n = 0; n < 30; n++) {
      this.list.push({
        id: Math.round(Math.random() * 10000).toString(),
        x: Math.random() * width,
        y: Math.random() * height,
       // rotation: Math.random() * 180,
       // scale: Math.random(),
        fill:"#"+((1<<24)*Math.random()|0).toString(16),
      })
    
          // console.log(this.$refs.layer2.getNode.batchDraw())
    }

        this.mainStage = this.$refs.stage.getNode();
        this.mainLayer = this.$refs.layer.getNode();
     
        console.log("this.mainLayer mount", this.mainLayer)
        document
        .getElementById('drag-items')
        .addEventListener('dragstart', (e) => {
          this.itemURL = e.target.src;
          console.log("this..", this)
          console.log("start  this.itemURL",  this.itemURL)
        });

      
      //gets the container div sourounding the stage


       var con = this.mainStage.container();
       con.addEventListener('dragover', function (e) {
        e.preventDefault(); // !important
      });

        let mainStage=  this.$refs.stage.getNode();
        let mainLayer = this.$refs.layer.getNode();

       con.addEventListener('drop',(e)=> {
        e.preventDefault();
        // now we need to find pointer position
        // we can't use stage.getPointerPosition() here, because that event
        // is not registered by Konva.Stage
        // we can register it manually:
        console.log("dropping");
          mainStage.setPointersPositions(e);
          console.log("mainStage ", mainStage);
          console.log("mainLayer", mainLayer);
          console.log("mainStage.getPointerPosition()", mainStage.getPointerPosition());
          console.log("this item url", this.itemURL)
          Konva.Image.fromURL(this.itemURL, function (image) {
            console.log("image is ", image)
          mainLayer.add(image);

          image.position(mainStage.getPointerPosition());
          image.draggable(true);

          console.log('mainLayeeer', mainLayer)
          mainLayer.draw();
          });
          // const image = new window.Image();
          // image.src = this.itemURL;
          // mainLayer.add(image);

          // image.position(mainStage.getPointerPosition());
          // image.draggable(true);

          // this.$refs.layer.getNode().draw();
        });
      




    },

      created() {
    const image = new window.Image();
    image.src = "gridTransp.png";
    image.onload = () => {
      // set image only when it is loaded
      this.image = image;
    };



  },

    //stg.add


};
</script>

<style>
body {
  margin: 0;
  padding: 0;
        background: linear-gradient(180deg, rgb(46, 46, 66) 0%, rgb(138, 177, 185) 100%);
        /* background-color: rgb(70, 74, 97); */

        
}
</style>

