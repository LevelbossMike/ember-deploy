---
title: Quickstart
---

Ember CLI Deploy works by executing functions that have been registered with [your application's deploy pipeline](../deploying-your-app).

You add new functionality by installing [plugins](/plugins) provided by the community - or writing your own.

Here's what an application's initial setup might look like:

```sh
# Ensure Ember CLI Deploy itself is installed
ember install ember-cli-deploy

# Install the Build plugin, which builds your app during deployment
ember install ember-cli-deploy-build

# Gzip our files
ember install ember-cli-deploy-gzip

# Install the S3 plugin, to upload our app to S3
ember install ember-cli-deploy-s3

# Install the S3-index plugin, to upload our `index.html` to S3
ember install ember-cli-deploy-s3-index
```

Sometimes, plugins require [configuration](../configuration). In this example, we need to give our S3 plugins our security credentials, and tell it which region and bucket to upload our app to:

```js
// config/deploy.js

module.exports = function(deployTarget) {
  var ENV = {};

  ENV['s3'] = {
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
    bucket: 'my-ember-app',
    region: 'us-east-1'
  };

  ENV['s3-index'] = {
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
    bucket: 'my-ember-app-index',
    region: 'us-east-1'
  };
};
```

Now, we can deploy our application. The default command deploys to the `production` target:

```sh
ember deploy
```

You can also specify a specific deploy target:

```sh
ember deploy staging
```

## Understanding your deployment strategy

Deployment concerns vary across applications and organizations. While Ember CLI Deploy does its best to bring conventions and structure to the deployment process, you'll inevitably need to customize your pipeline to suit your application's specific needs.

If you already have a good understanding of your deployment strategy and are ready to configure your pipeline, start by looking at the [list of community plugins](/plugins). You should always rely on existing plugins when you can, to save you time and prevent potential security issues. If a plugin doesn't exist for a certain part of your deployment process, you can always [write your own](../creating-a-plugin), and then compose it with other community plugins.

If you'd like some guidance on coming up with a good deployment strategy for your app, [read our guide](../determining-needs) on best practices and common issues that arise during deployment.
