---
layout: "post"
title: "Create Simple Image Upload Server in Node.js"
date: "2016-06-02 06:02"
---

1. Install node & npm
2. Install [express](http://expressjs.com/). `npm install express`
3. Install [multer](https://github.com/expressjs/multer). `npm install multer`

- (Optional) install [coffeescript](http://coffeescript.org/). `npm install -g coffeescript`

```
express = require 'express'
multer = require 'multer'
path = require 'path'
crypto = require 'crypto'

app = new express()

storage = multer.diskStorage {
  destination: './uploads'
  filename: (req, file, cb) ->
    crypto.pseudoRandomBytes 16, (err, raw) ->
      return cb(err) if err
      cb(null, "#{raw.toString 'hex'}#{path.extname file.originalname}")
}

app.post('/', multer({ storage: storage}).single('upload'), (req, res) ->
    console.log(req.file)
    console.log(req.body)
    res.status(204).end()
  )

app.listen 3000, console.log("Listening on port 3000")

```

- `storage` is used to define where the file will be stored and the file name. Multer didn't provide file extension, so if you want to, you can get it using path. _note: only use this in development / for testing only. Retrieving file extension from its name is bad practice. Never trust file extension given by uploader_
- I'm using `crypto` library for easier filenaming.
- Use multer with `storage` option in `post` `/` route
- `single('upload')` : when user upload a file (image), we expect the **image** has fieldname `upload`
- `log` the file and multipart body
- finally, make this app listen at port 3000

**Run the server.**

You can clone this project here : [https://github.com/hidrodixtion/ExampleMultipart](https://github.com/hidrodixtion/ExampleMultipart)
