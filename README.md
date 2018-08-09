# egg-kue

[![NPM version][npm-image]][npm-url]

[npm-image]: https://img.shields.io/npm/v/@giuem/egg-kue.svg?style=flat-square
[npm-url]: https://npmjs.org/package/@giuem/egg-kue

A priority job queue backed by redis, built for eggjs.

## Install

```bash
$ npm i @giuem/egg-kue --save
```

> For egg 1.x, use [egg-kue](https://www.npmjs.com/package/egg-kue) instead.

## Usage

```js
// {app_root}/config/plugin.js
exports.kue = {
  enable: true,
  package: '@giuem/egg-kue',
};
```

## Configuration

```js
// {app_root}/config/config.default.js
'use strict';
exports.kue = {
  app : true,
  agent : false,
  client: {
    queuePrefix: 'q',
    redis: {
      port: 6379,
      host: '127.0.0.1',
      auth: '',
      db: 3,
      // see https://github.com/mranney/node_redis#rediscreateclient
      options: {
      },
    },
  },
  // clients: {}
};
```

see [config/config.default.js](config/config.default.js) for more detail.

## Example

```js
app.kue.process('email', (job, done) => {
  // send email for this;
  email(job.data.to, done);
});

app.kue.create('email', {
    title: 'welcome email for justin'
  , to: 'gdjyluxiaoyong@gmail.com'
  , template: 'welcome-email'
}).save();
```
## License

[MIT](LICENSE)
