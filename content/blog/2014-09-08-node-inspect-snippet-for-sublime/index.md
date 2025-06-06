+++
title = "Node Inspect Snippet for Sublime"
+++

Is pretty common use console logs in nodejs to check the value of variables you are working on.

But only the `console.log` is not good enough some times. Mainly if the object you are checking has deep properties.

For these cases I usually use [`inspect`](http://nodejs.org/api/util.html#util_util_inspect_object_options) because it allows improve the log defining some options (`showHidden`, `depth`, `colors` and `customInspect`).

Due that I wrote a simple sublime snippet to help me create the logs:

```xml
<snippet>
  <content><![CDATA[
console.log(${1:'\n---->${2}', }require('util').inspect(${3:arguments}, { depth: null, colors: true }));
]]></content>
  <tabTrigger>inspect</tabTrigger>
  <scope>source.js</scope>
  <description>nodejs - util.inspect</description>
</snippet>
```

Typing `inspect` will generate this snippet:

```js
console.log("\n---->", require("util").inspect(obj, { depth: null, colors: true }));
```

Which will print something like this:

![Node Inspect](./node-inspect.png)
