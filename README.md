## restify-upload-file

a plugin for upload image file

### Install

```bash
npm i restify-upload-file
```

### Usage

#### server
```js
const corsMiddleware = require('restify-cors-middleware');
const app = restify.createServer();
app.use(restify.plugins.queryParser());
app.use(restify.plugins.bodyParser());

// allow cors with restify-cors-middleware
const cors = corsMiddleware({
  preflightMaxAge: 5, // Optional
  origins: ['http://localhost:8080'],
});
app.pre(cors.preflight);
app.use(cors.actual);

// fileUpload({ path: ... }) //set file upload path
//  default ./public/uploads/...
//  pass upload file info with req.info prop
app.post('/common/upload', fileUpload(), (req, res, next) => {
  res.send({
    code: 'success',
    info: req.info,
    message: 'file upload end!',
  });
  next();
});

```

#### client

Vue with axios

```vue
<template>
  <div class="upload-demo">
    <input type="file" ref="fileInt" @change="changeHandle">
  </div>
</template>

<script>

export default {
  name: 'UploadFileDemo',
  props: {
    msg: String
  },
  methods: {
    changeHandle() {
      const file = this.$refs.fileInt.files[0];
      console.log(file);
      const data = new FormData();
      data.append('file', file);
      axios.post('http://localhost:3006/common/upload', data, {
        headers: {
          'Content-Type': 'multipart/form-data',
        },
      }).then(res => {
        console.log(res);
      }).catch(err => {
        console.log(err);
      });
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

```
