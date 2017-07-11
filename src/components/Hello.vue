<template>
<div>
  <div class="uppy UppyDragDrop"></div>
   <div v-if='withProgress' class="UppyDragDrop-Progress"></div>
   <div class='uploaded-images' >
     <img v-for='img in images' :src='img.data.url' class='img' />
   </div>
</div>
</template>

<script>
const Uppy = require('uppy/lib/core/Core')
const DragDrop = require('uppy/lib/plugins/DragDrop')
const ProgressBar = require('uppy/lib/plugins/ProgressBar')
const Tus10 = require('uppy/lib/plugins/Tus10')
const uppy = new Uppy({debug: true})

export default {
  name: 'hello',
  props: {
    withProgress: { type: Boolean, default: true }
  },
  data () {
    return {
      images: [],
      bytesUploaded: 0,
      bytesTotal: 0,
      showProgress: false
    }
  },
  mounted () {
    let vm = this
    uppy
      .use(DragDrop, {target: '.UppyDragDrop'})
      .use(Tus10, {endpoint: '//master.tus.io/files/'})
      .use(ProgressBar, {target: '.UppyDragDrop-Progress'})
      .run()
    uppy.on('core:upload-progress', (data) => {
      vm.$emit('core:upload-progress', data)
      this.bytesUploaded = data.bytesUploaded
      // console.log(data.id, data.bytesUploaded, data.bytesTotal)
    })
    uppy.on('core:upload-success', (fileId, payload) => {
      let data = { fileId: fileId, data: payload }
      vm.$emit('core:upload-success', data)
      /* var img = new Image()
      img.width = 300
      img.alt = fileId
      img.src = url */
      this.images.push(data)
      this.showProgress = false
      // document.body.appendChild(img)
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.UppyDragDrop-Progress {
  position: relative;
}
.UppyDragDrop-Upload {
  display: block;
  margin: auto;
  padding: 5px 15px;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 1px;
  border: 0;
  border: 1px solid gray;
  background: none;
  cursor: pointer;
  margin-top: 15px;
}
.UppyDragDrop-Upload:hover {
  background: gray;
}
.img { max-width: 100px; }
</style>
