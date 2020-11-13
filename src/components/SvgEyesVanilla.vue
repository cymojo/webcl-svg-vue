<template>
  <div>
    <svg id="eye" viewBox="0 0 120 120" v-on:mousemove="follow(evt)">
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
  </div>
</template>

<script>
export default {
  name: "SvgEyesVanilla",
  data() {
    return {
      rect:document.querySelector("eye_iris ellipse")[0].getBoundingClientRect(),
      iris:document.querySelector("eye_iris"),
      xo:this.rect.x + this.rect.width/2,
      yo:this.rect.y + this.rect.height/2,
      xm:0,
      ym:0,
      xmax:this.rect.width/1.5,
      ymax:this.rect.height/2,
      widestFocus:400,
      scaledX:0,
      xe:0,
      scaledY:0,
      ye:0,
    }
  },
  methods: {
    follow(evt) {
      this.xm = evt.clientX;
      this.ym = evt.clientY;
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
      this.iris.style.transform = `translateX(${this.xe}px) translateY(${this.ye}px)`;
    }
  }
}

</script>

<style scoped>
svg {
  width:  100px;
  height: 80px;
  position: absolute;
}
#leftEye {
  top:  100px;
  left: 100px;
}
#rightEye {
  top:  100px;
  left: 250px;
}
</style>