<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import VueQrcode from '@chenfengyuan/vue-qrcode'
import vueLogo from './assets/logo.svg'

const logo = vueLogo;

function onReady(canvas: HTMLCanvasElement) {
  const context = canvas.getContext('2d')
  const image = new Image()

  image.src = logo;

  image.crossOrigin = 'anonymous'
  image.onload = () => {
    const coverage = .12
    const width = Math.round(canvas.width * coverage)
    const x = (canvas.width - width) / 2
    // @ts-ignore
    drawImage(context, image, x, x, width, width)

    canvas.addEventListener('click', () => downloadQRCode(canvas))
  }
}

function drawImage(
  context: CanvasRenderingContext2D,
  image: HTMLImageElement,
  x: number,
  y: number,
  width: number,
  height: number,
  radius = 0.5
) {
  context.shadowOffsetX = 0
  context.shadowOffsetY = 2
  context.shadowBlur = 4
  context.shadowColor = '#00000040'
  context.lineWidth = 8
  context.beginPath()
  context.moveTo(x + radius, y)
  context.arcTo(x + width, y, x + width, y + height, radius)
  context.arcTo(x + width, y + height, x, y + height, radius)
  context.arcTo(x, y + height, x, y, radius)
  context.arcTo(x, y, x + width, y, radius)
  context.closePath()
  context.strokeStyle = '#fff'
  context.stroke()
  context.clip()
  context.fillStyle = '#fff'
  context.fillRect(x, x, width, height)
  context.drawImage(image, x, x, width, height)
}

function downloadQRCode(canvas: HTMLCanvasElement) {
  const link = document.createElement('a')
  link.download = 'download.png'
  link.href = canvas.toDataURL()
  link.click()
  //  link.delete
}

function onReadySVG(svg: SVGElement) {
  svg.addEventListener('click', () => downloadSVG(svg))
}

function downloadSVG(svg: SVGElement) {
  //get svg source.
  const serializer = new XMLSerializer()
  let source = serializer.serializeToString(svg)

  //add name spaces.
  if (!source.match(/^<svg[^>]+xmlns="http:\/\/www\.w3\.org\/2000\/svg"/)) {
    source = source.replace(/^<svg/, '<svg xmlns="http://www.w3.org/2000/svg"')
  }

  if (!source.match(/^<svg[^>]+"http:\/\/www\.w3\.org\/1999\/xlink"/)) {
    source = source.replace(/^<svg/, '<svg xmlns:xlink="http://www.w3.org/1999/xlink"')
  }

  //change width height pixel to percent units
  if (source.match(/(width="[0-9]\d\d") (height="[0-9]\d\d")/)) {
    source = source.replace(
      /(width="[0-9]\d\d") (height="[0-9]\d\d")/,
      'width="100%" height="100%"'
    )
  }

  //add xml declaration
  source = '<?xml version="1.0" standalone="no"?>\r\n' + source

  //convert svg source to URI data scheme.
  const url = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(source)

  //set url value to a element's href attribute.
  const link = document.createElement('a')
  link.download = 'download.svg'
  link.href = url
  link.click() // trigger download
  //  link.delete
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main id="main">
    <div id="info">
      <h3>QR CODE Example</h3>
      <p>SVG</p>
      <p>CANVAS</p>
    </div>

    <!-- SVG -->
    <figure class="qrcode">
      <vue-qrcode
        value="https://www.xo.gr/#SVG"
        tag="svg"
        :options="{
          errorCorrectionLevel: 'Q',
          width: 200,
          color: {
            dark: '#40B883',
            light: '#1E1F22'
          }
        }"
        @ready="onReadySVG"
      ></vue-qrcode>
      <img
        class="qrcode__image"
        src="./assets/logo.svg"
        alt=""
      />
    </figure>

    <!-- Canvas -->
    <vue-qrcode
      value="https://www.xo.gr/#Canvas"
      :options="{
        errorCorrectionLevel: 'Q',
        width: 200,
        color: {
            dark: '#40B883',
            light: '#1E1F22'
        }
      }"
      @ready="onReady"
    ></vue-qrcode>
  </main>

</template>

