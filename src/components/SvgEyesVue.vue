<template>
  <div id="all-area" v-on:mousemove="follow">
    <svg id="eye" viewBox="0 0 120 120">
      <filter id="shadow">
        <feGaussianBlur in="SourceAlpha" stdDeviation="3" />
        <feOffset       dx="0" dy="8" />
        <feColorMatrix  type="matrix"
                        values="0 0 0 0  0
                                0 0 0 0  0
                                0 0 0 0  0
                                0 0 0 .5 0"/>
        <feBlend        in="SourceGraphic" mode="normal"/>
      </filter>
      <radialGradient id="gradient1" gradientUnits="objectBoundingBox" cx="50%" cy="50%" r="50%">
        <stop offset= "38%" stop-color="#000000" stop-opacity="1" />
        <stop offset= "46%" stop-color="#073F80" stop-opacity="1" />
        <stop offset= "90%" stop-color="#8EC0DD" stop-opacity="1" />
        <stop offset="100%" stop-color="#2F3A46" stop-opacity="1" />
      </radialGradient>
      <g id="eye_iris">
        <ellipse cx="60" cy="60" rx="30" ry="30" opacity="1" fill="url(#gradient1)" />
        <ellipse cx="50" cy="50" rx="7"  ry="7"  opacity="1" fill="#FFFFFF" fill-opacity="0.8"/>
      </g>
      <g id="eye_openLids">
        <path d="M0 60 A60,60 0 0,1 120,60 A60,30 0 0,0 0,60 Z" opacity="1" fill="#FDDC99" fill-opacity="1" filter="url(#shadow)" />
        <path d="M0 60 A60,60 0 0,0 120,60 A60,40 0 0,1 0,60 Z" opacity="1" fill="#F4CB76" fill-opacity="1" />
      </g>
    </svg>
    <svg id="eye2" viewBox="0 0 120 120">
      <filter id="shadow">
        <feGaussianBlur in="SourceAlpha" stdDeviation="3" />
        <feOffset       dx="0" dy="8" />
        <feColorMatrix  type="matrix"
                        values="0 0 0 0  0
                                0 0 0 0  0
                                0 0 0 0  0
                                0 0 0 .5 0"/>
        <feBlend        in="SourceGraphic" mode="normal"/>
      </filter>
      <radialGradient id="gradient1" gradientUnits="objectBoundingBox" cx="50%" cy="50%" r="50%">
        <stop offset= "38%" stop-color="#000000" stop-opacity="1" />
        <stop offset= "46%" stop-color="#073F80" stop-opacity="1" />
        <stop offset= "90%" stop-color="#8EC0DD" stop-opacity="1" />
        <stop offset="100%" stop-color="#2F3A46" stop-opacity="1" />
      </radialGradient>
      <g id="eye2_iris">
        <ellipse cx="60" cy="60" rx="30" ry="30" opacity="1" fill="url(#gradient1)" />
        <ellipse cx="50" cy="50" rx="7"  ry="7"  opacity="1" fill="#FFFFFF" fill-opacity="0.8"/>
      </g>
      <g id="eye2_openLids">
        <path d="M0 60 A60,60 0 0,1 120,60 A60,30 0 0,0 0,60 Z" opacity="1" fill="#FDDC99" fill-opacity="1" filter="url(#shadow)" />
        <path d="M0 60 A60,60 0 0,0 120,60 A60,40 0 0,1 0,60 Z" opacity="1" fill="#F4CB76" fill-opacity="1" />
      </g>
    </svg>
  </div>
</template>

<script>
  export default {
    name: "SvgEyesVue",
    data() {
      return {
        x:130,
        y:470,
        width:40,
        height:40,
        xo:0,
        yo:0,
        xm:0,
        ym:0,
        xmax:0,
        ymax:0,
        widestFocus:400,
        scaledX:0,
        xe:0,
        scaledY:0,
        ye:0,
      }
    },
    methods: {
      follow(evt) {

        /* Eye one */
        this.xo = this.x + this.width/2;
        this.yo = this.y + this.height/2;
        this.xmax = this.width/1.5;
        this.ymax = this.height/2;

        this.xm = evt.clientX - this.xo;
        this.ym = evt.clientY - this.yo;

        console.log(`Mouse x: ${this.xm}, Mouse y ${this.ym}`);

        this.scaledX = this.xm * (this.xmax / this.widestFocus );

        this.xe = this.xm > 0
                ? Math.min( this.xmax, this.scaledX)
                : Math.max(-this.xmax, this.scaledX);
        this.scaledY = this.ym * (this.ymax / this.widestFocus );

        this.ye = this.ym > 0
                ? Math.min( this.ymax, this.scaledY)
                : Math.max(-this.ymax, this.scaledY);
        if (this.xe*this.xe + this.ye*this.ye > this.xmax * this.ymax) {
          this.xe *= 0.9;
          this.ye *= 0.9;
        }

        document.getElementById("eye_iris").style.visibility = "visible";
        document.getElementById("eye_iris").style.transform = `translateX(${this.xe}px) translateY(${this.ye}px)`;
        //this.iris.style.transform = `translateX(${this.xe}px) translateY(${this.ye}px)`;

        /* Eye 2 */
        document.getElementById("eye2_iris").style.visibility = "visible";
        document.getElementById("eye2_iris").style.transform = `translateX(${this.xe}px) translateY(${this.ye}px)`;
        //this.iris.style.transform = `translateX(${this.xe}px) translateY(${this.ye}px)`;
      }
    }
  }

</script>

<style scoped>
  #eye {
    width:  100px;
    height: 80px;
    position: absolute;
    left: 100px;
    top: 450px;
  }
  #eye2 {
    width:  100px;
    height: 80px;
    position: absolute;
    left: 200px;
    top: 450px;
  }
  #all-area {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
  }
  #eye_iris {
    visibility: hidden;
  }
  #eye2_iris {
    visibility: hidden;
  }
</style>