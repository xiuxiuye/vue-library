<style scoped>
.wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.validate-move-block {
  position: absolute;
  border-radius: 4px;
  z-index: 15;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 1);
}
.validate-target-block {
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 10;
  border-radius: 4px;
  position: absolute;
  box-shadow: 4px 4px 10px 0px rgba(0, 0, 0, 1) inset;
}
.slide-rail {
  height: 40px;
  background-color: #dcdee2;
  border-radius: 24px;
  margin-top: 30px;
  position: relative;
  box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.6) inset;
}
.slide-block {
  background-color: white;
  border-radius: 50%;
  position: absolute;
  top: -5px;
  box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 1);
}
</style>

<template>
  <div class="wrapper">
    <div
      :style="{
          width: `${styleDatas.imageWidth}px`,
          height: `${styleDatas.imageHeight}px`,
          'background-image': `url(${dynamicLoadImg(styleDatas.bgImageName)})`,
          position: 'relative',
          'border-radius': '4px'
        }"
    >
      <div
        class="validate-move-block"
        :style="{
            width: `${styleDatas.subBlockWidth}px`,
            height: `${styleDatas.subBlockHeight}px`,
            top: `${styleDatas.randomTop}px`,
            left:  `${styleDatas.moveBlockLeft + 224}px`,
            'background-image': `url(${dynamicLoadImg(styleDatas.bgImageName)})`,
            'background-size': `${styleDatas.imageWidth}px ${styleDatas.imageHeight}px`,
            'background-position-y': `-${styleDatas.randomTop}px`,
            'background-position-x': `-${styleDatas.randomLeft}px`
        }"
      ></div>
      <div
        class="validate-target-block"
        :style="{
            width: `${this.styleDatas.subBlockWidth}px`,
            height: `${this.styleDatas.subBlockHeight}px`,
            top: `${this.styleDatas.randomTop}px`,
            left: `${this.styleDatas.randomLeft}px`
        }"
      ></div>
    </div>
    <div class="slide-rail" :style="{ width: `${styleDatas.imageWidth}px` }">
      <div
        id="clickme"
        class="slide-block"
        :style="{
            width: `${styleDatas.slideBtnWidth}px`,
            height: `${styleDatas.slideBtnHeight}px`,
            left: `${styleDatas.moveBlockLeft+4}px`
        }"
        @mousedown="startDrag($event)"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      styleDatas: {},
      verifyWrapperStyle: {},
      targetPonitX: null
    };
  },
  methods: {
    init() {
      this.initStyleDatas();
    },
    initStyleDatas() {
      this.styleDatas = {
        imageWidth: 400,
        imageHeight: 300,
        subBlockWidth: 60,
        subBlockHeight: 60,
        bgImageName: "img.jpg",
        randomTop: 0,
        randomLeft: 0,
        moveBlockLeft: 0,
        slideBtnWidth: 50,
        slideBtnHeight: 50
      };
      this.styleDatas.randomTop = Math.floor(
        Math.random() *
          (this.styleDatas.imageHeight - this.styleDatas.subBlockHeight)
      );
      this.styleDatas.randomLeft = Math.floor(
        Math.random() *
          (this.styleDatas.imageWidth - this.styleDatas.subBlockWidth - 160) +
          160
      );
      this.targetPonitX =
        this.styleDatas.randomLeft + this.styleDatas.subBlockWidth / 2;
    },
    dynamicLoadImg(imgName) {
      return require(`../assets/${imgName}`);
    },
    startDrag($event) {
      let startPointX = $event.clientX;
      document.onmouseup = () => {
        this.endDrag();
      };
      document.onmousemove = event => {
        let endPointX = event.clientX;
        //compute x
        this.handleMouseMove(startPointX, endPointX);
      };
    },
    handleMouseMove(startPointX, endPointX) {
      if (endPointX > startPointX) {
        if (
          endPointX - startPointX <=
          this.styleDatas.imageWidth - this.styleDatas.subBlockWidth
        ) {
          this.styleDatas.moveBlockLeft = endPointX - startPointX;
        } else {
          this.styleDatas.moveBlockLeft =
            this.styleDatas.imageWidth - this.styleDatas.subBlockWidth;
        }
      } else {
        this.styleDatas.moveBlockLeft = 0;
      }
    },
    endDrag() {
      document.querySelector("#clickme").click();
      document.onmousemove = null;
      document.onmouseup = null;
      //验证
      this.validate();
    },
    validate() {
    //   let currentX =
    //     this.styleDatas.moveBlockLeft + this.styleDatas.subBlockWidth / 2;
    //   if (Math.abs(currentX - this.targetPonitX) < 30) {
    //     alert(1);
    //   } else {
    //     alert(2);
    //   }
      this.init();
    },
    stopDefault($event) {
      $event.preventDefault();
    }
  },
  mounted() {},
  created() {
    this.init();
  }
};
</script>