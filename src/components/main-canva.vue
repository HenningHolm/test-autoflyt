<template>
  <div style="overflow: hidden" id="stage-container"  @wheel="resize">

  </div>
</template>
<script>

import Konva from 'konva';


export default {
    name: 'MainCanva',
  data() {
    return {
      list: [],
      mainStage : undefined,
      gridLayer: undefined,
      drawLayer: undefined,
      dragItemId: "",
      itemUrl : null, //rename
      retotus: undefined
    };
  },

  methods: {

    resize(e){
    var stage = this.mainStage; 
    var stageXScale= stage.scaleX()- e.deltaY/2000;
    var stageYScale= stage.scaleY()- e.deltaY/2000;
    
    stage.scale({ x: stageXScale, y:stageYScale })
    stage.batchDraw();
    },

    drawMultiSelect(e){ 
      console.log("e", e);

      }

  },
  mounted() {

    //-----------------------------------------------------------------//
    //--------------------------Setup mainStage -----------------------//
    //-----------------------------------------------------------------//

    let stage = new Konva.Stage(
    {
        container: "stage-container",
        width: 4000,
        height: 4000,
        draggable: true,
    });
      
    //-------MainStage eventlisteners-------//

    // Put shape in front by double click
    this.mainStage = stage;
    stage.on("dblclick", (e) =>{ e.target.moveToTop()});

    // Multiselect objects by shift + leftclick and draw
    stage.on('dragstart', (e) => {
    if (e.evt.shiftKey) {
      stage.stopDrag();
    this.drawMultiSelect(e);
    console.log("drawMultiSelect")
    } else {
      console.log('normally drag');
    }
    })
    // ----------------------------------------------------------------//
    // ----------------------------------------------------------------//


    //--------Setup GridLayer-------//

    let gridLayer = new Konva.Layer({container: 'layer-container'});
    this.gridLayer = gridLayer;
    stage.add(gridLayer);

      Konva.Image.fromURL(
      'gridTransp.png',
      (img) => {
        img.setAttrs({
          x: 0,
          y: 0,
          name: 'image',
          draggable: false,
        });

        gridLayer.add(img);
        stage.draw()
      });
        

    //--------Setup ObjectLayer--------//

    let drawLayer = new Konva.Layer({container: 'layer-container'});
    this.drawLayer = drawLayer;
    stage.add(drawLayer);

    //-------Add Test Elements---------// 
    
    let rect = new Konva.Rect({
      x : 300,
      y : 300,
      fill : "blue",
      width : 160,
      height: 80,
      stroke: "orange", 
      draggable: true,
      container: "rect-container"
    });

    let rect2 = new Konva.Rect({
      x : 400,
      y : 400,
      fill : "green",
      width : 160,
      height: 80,
      stroke: "orange", 
      draggable: true,
      container: "rect-container"
    })
    rect.on("click", () => {console.log(rect.fill())})
    drawLayer.add(rect,rect2);
    stage.batchDraw()


    },


};
</script>

<style>

</style>

