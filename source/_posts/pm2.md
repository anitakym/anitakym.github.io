---
title: pm2
date: 2021-06-29 15:24:15
tags:
---

## 源码分析
### cluster
```
// lib/God.js
var cluster       = require('cluster');
require('./God/ClusterMode.js')(God);
/**
     * Cluster mode logic (for NodeJS apps)
     */
...
// ./God/ClusterMode.js
module.exports = function ClusterMode(God) {

  /**
   * For Node apps - Cluster mode
   * It will wrap the code and enable load-balancing mode
   * @method nodeApp
   * @param {} env_copy
   * @param {} cb
   * @return Literal
   */
  God.nodeApp = function nodeApp(env_copy, cb){
    var clu = null;

    console.log(`App [${env_copy.name}:${env_copy.pm_id}] starting in -cluster mode-`)
    if (env_copy.node_args && Array.isArray(env_copy.node_args)) {
      cluster.settings.execArgv = env_copy.node_args;
    }

    env_copy._pm2_version = pkg.version;

    try {
      // node.js cluster clients can not receive deep-level objects or arrays in the forked process, e.g.:
      // { "args": ["foo", "bar"], "env": { "foo1": "bar1" }} will be parsed to
      // { "args": "foo, bar", "env": "[object Object]"}
      // So we passing a stringified JSON here.
      clu = cluster.fork({pm2_env: JSON.stringify(env_copy), windowsHide: true});
    } catch(e) {
      God.logAndGenerateError(e);
      return cb(e);
    }

    clu.pm2_env = env_copy;

    /**
     * Broadcast message to God
     */
    clu.on('message', function cluMessage(msg) {
      /*********************************
       * If you edit this function
       * Do the same in ForkMode.js !
       *********************************/
      if (msg.data && msg.type) {
        return God.bus.emit(msg.type ? msg.type : 'process:msg', {
          at      : Utility.getDate(),
          data    : msg.data,
          process :  {
            pm_id      : clu.pm2_env.pm_id,
            name       : clu.pm2_env.name,
            rev        : (clu.pm2_env.versioning && clu.pm2_env.versioning.revision) ? clu.pm2_env.versioning.revision : null,
            namespace  : clu.pm2_env.namespace
          }
        });
      }
      else {

        if (typeof msg == 'object' && 'node_version' in msg) {
          clu.pm2_env.node_version = msg.node_version;
          return false;
        }

        return God.bus.emit('process:msg', {
          at      : Utility.getDate(),
          raw     : msg,
          process :  {
            pm_id      : clu.pm2_env.pm_id,
            name       : clu.pm2_env.name,
            namespace  : clu.pm2_env.namespace
          }
        });
      }
    });

    return cb(null, clu);
  };
};

```
我们还可以看下cluster mode的测试用例
### God.js的依赖
```
var cluster       = require('cluster');
var numCPUs       = require('os').cpus() ? require('os').cpus().length : 1;
var path          = require('path');
var EventEmitter2 = require('eventemitter2').EventEmitter2;
var fs            = require('fs');
var vizion        = require('vizion');
var debug         = require('debug')('pm2:god');
var Utility       = require('./Utility');
var cst           = require('../constants.js');
var timesLimit    = require('async/timesLimit');
var Configuration = require('./Configuration.js');
var semver        = require('semver');
```
#### semver
```
/**
 * Override cluster module configuration
 */
if (semver.lt(process.version, '10.0.0')) {
  cluster.setupMaster({
    windowsHide: true,
    exec : path.resolve(path.dirname(module.filename), 'ProcessContainerLegacy.js')
  });
}
else {
  cluster.setupMaster({
    windowsHide: true,
    exec : path.resolve(path.dirname(module.filename), 'ProcessContainer.js')
  });
}
```
显然，semver(1) -- The semantic versioner for npm，用作判断版本
#### vizion
- Git/Subversion/Mercurial repository metadata parser
- Grab metadata for svn/git/hg repositories ```vizion.analyze```
- Check if a local repository is up to date with its remote```vizion.isUpToDate```
- Update the local repository to latest commit found on the remote for its current branch on fail it rollbacks to the latest commit```vizion.update```
- Revert to a specified commit```revertTo```
- ...等功能
God.js中用到了analyze, 目标是：Discovers if your app is a svn/git/hg repository and shows metadata about it

```

/**
 * Grab metadata for svn/git/hg repositories
 */
vizion.analyze({
  folder : '/tmp/folder'
}, function(err, meta) {
  if (err) throw new Error(err);

  /**
   *
   * meta = {
   *   type        : 'git',
   *   ahead       : false,
   *   unstaged    : false,
   *   branch      : 'development',
   *   remotes     : [ 'http', 'http ssl', 'origin' ],
   *   remote      : 'origin',
   *   commment    : 'This is a comment',
   *   update_time : Tue Oct 28 2014 14:33:30 GMT+0100 (CET),
   *   url         : 'https://github.com/keymetrics/vizion.git',
   *   revision    : 'f0a1d45936cf7a3c969e4caba96546fd23255796',
   *   next_rev    : null,  // null if its latest in the branch
   *   prev_rev    : '6d6932dac9c82f8a29ff40c1d5300569c24aa2c8'
   * }
   *
   */
});
```
```
// God.js
vizion.analyze({folder : current_path}, function recur_path(err, meta){
    var proc = God.clusters_db[proc_id];

    if (err)
      debug(err.stack || err);

    if (!proc ||
        !proc.pm2_env ||
        proc.pm2_env.status == cst.STOPPED_STATUS ||
        proc.pm2_env.status == cst.STOPPING_STATUS ||
        proc.pm2_env.status == cst.ERRORED_STATUS) {
      return console.error('Cancelling versioning data parsing');
    }

    proc.pm2_env.vizion_running = false;

    if (!err) {
      proc.pm2_env.versioning = meta;
      proc.pm2_env.versioning.repo_path = current_path;
      God.notify('online', proc);
    }
    else if (err && current_path === last_path) {
      proc.pm2_env.versioning = null;
      God.notify('online', proc);
    }
    else {
      last_path = current_path;
      current_path = path.dirname(current_path);
      proc.pm2_env.vizion_running = true;
      vizion.analyze({folder : current_path}, recur_path);
    }
    return false;
  });
```


## 项目使用
### 日志配置
- ecosystem file 
 - merge_logs | log | log_Date_format
 - pm2 install pm2-logrotate && pm2 set pm2-logrotate:retain 14
 - scripts: pm2 start ecosystem.config.js --env xxx (dev + --watch)


 ## basic 介绍
 ### pm2 list
 #### uptime
 运行时间
 #### restarts
 重启次数


 ## 监控
 ### pm2.IO
 - 官方：keymetrics, 有免费的配额（You can now connect up to 4 servers or Node.js processes for free.）
 - 免费的限制服务数量，且功能较少，里面还会有plus和enterprise版本的供选购
 - https://pm2.keymetrics.io/docs/usage/docker-pm2-nodejs/
 - https://app.pm2.io/
 ```
 # server
 pm2 link xxx-sec-key xxx-pub-key
 # docker
 RUN npm install pm2 -g
 ENV PM2_PUBLIC_KEY xxx
 ENV PM2_SECRET_KEY xxx

 CMD ["pm2-runtime", "app.js"]
 # pm2 link
 pm2 link -h

  Usage: link [options] [secret] [public] [name]

  link with the pm2 monitoring dashboard

  Options:

    --info-node [url]  set url info node
    --ws               websocket mode
    --axon             axon mode
    -h, --help         output usage information
 ```

 