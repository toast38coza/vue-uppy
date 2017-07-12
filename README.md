# vue-uppy

> A vue wrapper for uppy.io

This ia more of a proof of concept than anything production ready .. but it works :).

## Installation

You'll need [uppy](http://uppy.io):

```
npm install --save uppy
```

## Usage:

```
import Uppy from `vue-uppy/src/components/Uppy`
...

<uppy
	@core:upload-progress=updateProgressStatus
	@core:upload-success=imageUploaded
	@core:success=allImagesUploaded
	:with-progress='true' ></uppy>
```

**Events:**

* `core:upload-progress` = sends bytes and totalbytes
* `core:upload-success` = sends all data about the image, including the url on [tus.io](http://tus.io) where it has been uploaded
* `core:success` = sends file count

**Props:**

* `with-progress` -> whether or not to show the progress bar

Feel free to just grap `src/components/Uppy.vue` and put it in your project.



## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
