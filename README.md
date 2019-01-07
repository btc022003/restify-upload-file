## restify-upload-file

a plugin for upload image file

### Install

```bash
npm i restify-upload-file
```

### Usage

```js
const app = restify.createServer();
app.use(restify.plugins.queryParser());
app.use(restify.plugins.bodyParser());

// fileUpload({ path: ... }) //set file upload path
//  default ./public/uploads/...

app.post('/common/upload', fileUpload(), (req, res, next) => {
  res.send({
    code: 'success',
    info: req.info,
    message: 'file upload end!',
  });
  next();
});

```
