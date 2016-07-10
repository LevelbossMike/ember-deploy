---
title: Upgrading
---
## Upgrading an App from 0.6.X to 1.0.x

Verify your plugins are 1.0.x compatible by checking the badge on their README.

1.0.x brings new [configuration options](../configuration) for your plugin ordering that you can use.

### Upgrade the `plugins` config

The old `plugins` [config option](/docs/v0.6.x/aliasing-plugins/) is now deprecated.

To deprecated

```js
ENV.plugins = ['build', 'redis'];
```

becomes

```js
ENV.pipeline = {
  disabled: {
    allExcept: ['build', 'redis']
  }
};
```

The new aliasing configuration is described in [the cookbook](../including-a-plugin-twice/)

## Upgrading an App from 0.5.X to 0.6.x

Verify your plugins are 0.6.x compatible by checking the badge on their README. No other changes should be required.

## Upgrading an App from 0.4.X to 0.5.x

### Upgrade an app that uses the Lightning strategy

To upgrade an application that used the Lightning Strategy in 0.4.X:

* replace `ember-deploy-redis` with `ember-cli-deploy-redis`
* remove store key in config and replace with plugin specific key (`redis`)
* replace `ember-deploy-s3` with `ember-cli-deploy-s3`
* upgrade `config/deploy.js` format, see new [blueprint](https://github.com/ember-cli-deploy/ember-cli-deploy/blob/master/blueprints/ember-cli-deploy/files/config/deploy.js)
* assets renamed to s3
* install `ember-cli-deploy-build`
* add new `dotenv` files `.env.build.environment`
* add `ember-cli-deploy-revision-data`
* add `ember-cli-deploy-display-revisions`

#### Notes:

For the redis plugin the default key is now `app:index:current` and the key is not stored with the full path just the short commit hash.

For an example of a full upgrade see [this commit](https://github.com/ghedamat/ember-deploy-demo/commit/ad74274839a30641a5d4612a790eb8ab8007d80f) on the ember-deploy-demo repo.
