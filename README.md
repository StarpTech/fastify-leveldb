# fastify-leveldb

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](http://standardjs.com/)  [![Build Status](https://travis-ci.org/fastify/fastify-leveldb.svg?branch=master)](https://travis-ci.org/fastify/fastify-leveldb)


Fastify LevelDB connection plugin, with this you can share the same Level connection in every part of your server.

Under the hood [Level](https://github.com/Level/level) is used, the options that you pass to register will be passed to Level.

## Install
```
npm i fastify-leveldb --save
```
## Usage
Add it to you project with `register` and you are done!  
You can access LevelDB via `fastify.level`.
```js
const fastify = require('fastify')

fastify.register(require('fastify-leveldb'), {
  name: 'db'
}, err => {
  if (err) throw err
})

fastify.get('/foo', (req, reply) => {
  const { level } = fastify
  level.get(req.query.key, (err, val) => {
    reply.send(err || val)
  })
})

fastify.post('/foo', (req, reply) => {
  const { level } = fastify
  level.put(req.body.key, req.body.value, (err) => {
    reply.send(err || { status: 'ok' })
  })
})

fastify.listen(3000, err => {
  if (err) throw err
  console.log(`server listening on ${fastify.server.address().port}`)
})
```

## Acknowledgements

This project is kindly sponsored by:
- [nearForm](http://nearform.com)
- [LetzDoIt](http://www.letzdoitapp.com/)

## License

Licensed under [MIT](./LICENSE).
