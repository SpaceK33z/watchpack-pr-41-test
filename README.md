This is about [watchpack PR 41](https://github.com/webpack/watchpack/pull/41)

```
npm install
npm start
```

After starting, you should see this:

```
ERROR in ./entry.js
Module not found: Error: Can't resolve 'asdfasdf' in '/Users/kees/dev/watchpack-pr-41-test'
 @ ./entry.js 1:0-18
 @ multi (webpack)-dev-server/client?http://localhost:8080 ./entry.js
webpack: bundle is now VALID.
```

**But note that the process keeps running (which is correct).**

Now, in a separate folder, do this:

```
git clone https://github.com/wtgtybhertgeghgtwtg/watchpack.git
cd watchpack
npm i
npm link
```

Go back to this test repository and do:

```
npm link watchpack
npm start
```

Now you should see something like this:

```
fs.js:1431
    throw error;
    ^

Error: watch /Users/kees/dev/node_modules/asdfasdf ENOENT
    at exports._errnoException (util.js:1026:11)
    at FSWatcher.start (fs.js:1429:19)
    at Object.fs.watch (fs.js:1456:11)
    at NodeWatcher.watchdir (/Users/kees/dev/watchpack/node_modules/sane/src/node_watcher.js:148:20)
    at new NodeWatcher (/Users/kees/dev/watchpack/node_modules/sane/src/node_watcher.js:45:8)
    at sane (/Users/kees/dev/watchpack/node_modules/sane/index.js:17:12)
    at new DirectoryWatcher (/Users/kees/dev/watchpack/lib/DirectoryWatcher.js:49:17)
    at WatcherManager.getDirectoryWatcher (/Users/kees/dev/watchpack/lib/watcherManager.js:16:33)
    at WatcherManager.watchFile (/Users/kees/dev/watchpack/lib/watcherManager.js:26:14)
    at EventEmitter.<anonymous> (/Users/kees/dev/watchpack/lib/watchpack.js:36:49)

```

Which is a fatal error and the process stops. It should behave the same as shown above.
