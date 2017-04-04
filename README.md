# api documentation for  [ip (v1.1.5)](https://github.com/indutny/node-ip)  [![npm package](https://img.shields.io/npm/v/npmdoc-ip.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-ip) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-ip.svg)](https://travis-ci.org/npmdoc/node-npmdoc-ip)
#### [![](https://badge.fury.io/js/ip.svg)](https://www.npmjs.com/package/ip)

[![NPM](https://nodei.co/npm/ip.png?downloads=true)](https://www.npmjs.com/package/ip)

[![apidoc](https://npmdoc.github.io/node-npmdoc-ip/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-ip_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-ip/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-ip/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-ip/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Fedor Indutny",
        "email": "fedor@indutny.com"
    },
    "bugs": {
        "url": "https://github.com/indutny/node-ip/issues"
    },
    "dependencies": {},
    "description": "[![](https://badge.fury.io/js/ip.svg)](https://www.npmjs.com/package/ip)",
    "devDependencies": {
        "jscs": "^2.1.1",
        "jshint": "^2.8.0",
        "mocha": "~1.3.2"
    },
    "directories": {},
    "dist": {
        "shasum": "bdded70114290828c0a039e72ef25f5aaec4354a",
        "tarball": "https://registry.npmjs.org/ip/-/ip-1.1.5.tgz"
    },
    "gitHead": "43e442366bf5a93493c8c4c36736f87d675b0c3d",
    "homepage": "https://github.com/indutny/node-ip",
    "license": "MIT",
    "main": "lib/ip",
    "maintainers": [
        {
            "name": "bcbailey",
            "email": "brad@memoryleak.org"
        },
        {
            "name": "fedor.indutny",
            "email": "fedor.indutny@gmail.com"
        },
        {
            "name": "indexzero",
            "email": "charlie.robbins@gmail.com"
        },
        {
            "name": "indutny",
            "email": "fedor@indutny.com"
        },
        {
            "name": "mmalecki",
            "email": "me@mmalecki.com"
        }
    ],
    "name": "ip",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/indutny/node-ip.git"
    },
    "scripts": {
        "fix": "jscs lib/*.js test/*.js --fix",
        "test": "jscs lib/*.js test/*.js && jshint lib/*.js && mocha --reporter spec test/*-test.js"
    },
    "version": "1.1.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module ip](#apidoc.module.ip)
1.  [function <span class="apidocSignatureSpan">ip.</span>address (name, family)](#apidoc.element.ip.address)
1.  [function <span class="apidocSignatureSpan">ip.</span>cidr (cidrString)](#apidoc.element.ip.cidr)
1.  [function <span class="apidocSignatureSpan">ip.</span>cidrSubnet (cidrString)](#apidoc.element.ip.cidrSubnet)
1.  [function <span class="apidocSignatureSpan">ip.</span>fromLong (ipl)](#apidoc.element.ip.fromLong)
1.  [function <span class="apidocSignatureSpan">ip.</span>fromPrefixLen (prefixlen, family)](#apidoc.element.ip.fromPrefixLen)
1.  [function <span class="apidocSignatureSpan">ip.</span>isEqual (a, b)](#apidoc.element.ip.isEqual)
1.  [function <span class="apidocSignatureSpan">ip.</span>isLoopback (addr)](#apidoc.element.ip.isLoopback)
1.  [function <span class="apidocSignatureSpan">ip.</span>isPrivate (addr)](#apidoc.element.ip.isPrivate)
1.  [function <span class="apidocSignatureSpan">ip.</span>isPublic (addr)](#apidoc.element.ip.isPublic)
1.  [function <span class="apidocSignatureSpan">ip.</span>isV4Format (ip)](#apidoc.element.ip.isV4Format)
1.  [function <span class="apidocSignatureSpan">ip.</span>isV6Format (ip)](#apidoc.element.ip.isV6Format)
1.  [function <span class="apidocSignatureSpan">ip.</span>loopback (family)](#apidoc.element.ip.loopback)
1.  [function <span class="apidocSignatureSpan">ip.</span>mask (addr, mask)](#apidoc.element.ip.mask)
1.  [function <span class="apidocSignatureSpan">ip.</span>not (addr)](#apidoc.element.ip.not)
1.  [function <span class="apidocSignatureSpan">ip.</span>or (a, b)](#apidoc.element.ip.or)
1.  [function <span class="apidocSignatureSpan">ip.</span>subnet (addr, mask)](#apidoc.element.ip.subnet)
1.  [function <span class="apidocSignatureSpan">ip.</span>toBuffer (ip, buff, offset)](#apidoc.element.ip.toBuffer)
1.  [function <span class="apidocSignatureSpan">ip.</span>toLong (ip)](#apidoc.element.ip.toLong)



# <a name="apidoc.module.ip"></a>[module ip](#apidoc.module.ip)

#### <a name="apidoc.element.ip.address"></a>[function <span class="apidocSignatureSpan">ip.</span>address (name, family)](#apidoc.element.ip.address)
- description and source-code
```javascript
address = function (name, family) {
  var interfaces = os.networkInterfaces();
  var all;

  //
  // Default to 'ipv4'
  //
  family = _normalizeFamily(family);

  //
  // If a specific network interface has been named,
  // return the address.
  //
  if (name && name !== 'private' && name !== 'public') {
    var res = interfaces[name].filter(function(details) {
      var itemFamily = details.family.toLowerCase();
      return itemFamily === family;
    });
    if (res.length === 0)
      return undefined;
    return res[0].address;
  }

  var all = Object.keys(interfaces).map(function (nic) {
    //
    // Note: name will only be 'public' or 'private'
    // when this is called.
    //
    var addresses = interfaces[nic].filter(function (details) {
      details.family = details.family.toLowerCase();
      if (details.family !== family || ip.isLoopback(details.address)) {
        return false;
      } else if (!name) {
        return true;
      }

      return name === 'public' ? ip.isPrivate(details.address) :
          ip.isPublic(details.address);
    });

    return addresses.length ? addresses[0].address : undefined;
  }).filter(Boolean);

  return !all.length ? ip.loopback(family) : all[0];
}
```
- example usage
```shell
...

## Usage
Get your ip address, compare ip addresses, validate ip addresses, etc.

'''js
var ip = require('ip');

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
...
```

#### <a name="apidoc.element.ip.cidr"></a>[function <span class="apidocSignatureSpan">ip.</span>cidr (cidrString)](#apidoc.element.ip.cidr)
- description and source-code
```javascript
cidr = function (cidrString) {
  var cidrParts = cidrString.split('/');

  var addr = cidrParts[0];
  if (cidrParts.length !== 2)
    throw new Error('invalid CIDR subnet: ' + addr);

  var mask = ip.fromPrefixLen(parseInt(cidrParts[1], 10));

  return ip.mask(addr, mask);
}
```
- example usage
```shell
...

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
...
```

#### <a name="apidoc.element.ip.cidrSubnet"></a>[function <span class="apidocSignatureSpan">ip.</span>cidrSubnet (cidrString)](#apidoc.element.ip.cidrSubnet)
- description and source-code
```javascript
cidrSubnet = function (cidrString) {
  var cidrParts = cidrString.split('/');

  var addr = cidrParts[0];
  if (cidrParts.length !== 2)
    throw new Error('invalid CIDR subnet: ' + addr);

  var mask = ip.fromPrefixLen(parseInt(cidrParts[1], 10));

  return ip.subnet(addr, mask);
}
```
- example usage
```shell
...
//   lastAddress: '192.168.1.190',
//   broadcastAddress: '192.168.1.191',
//   subnetMask: '255.255.255.192',
//   subnetMaskLength: 26,
//   numHosts: 62,
//   length: 64,
//   contains: function(addr){...} }
ip.cidrSubnet('192.168.1.134/26')
// Same as previous.

// range checking
ip.cidrSubnet('192.168.1.134/26').contains('192.168.1.190') // true


// ipv4 long conversion
...
```

#### <a name="apidoc.element.ip.fromLong"></a>[function <span class="apidocSignatureSpan">ip.</span>fromLong (ipl)](#apidoc.element.ip.fromLong)
- description and source-code
```javascript
fromLong = function (ipl) {
  return ((ipl >>> 24) + '.' +
      (ipl >> 16 & 255) + '.' +
      (ipl >> 8 & 255) + '.' +
      (ipl & 255) );
}
```
- example usage
```shell
...

// range checking
ip.cidrSubnet('192.168.1.134/26').contains('192.168.1.190') // true


// ipv4 long conversion
ip.toLong('127.0.0.1'); // 2130706433
ip.fromLong(2130706433); // '127.0.0.1'
'''

### License

This software is licensed under the MIT License.

Copyright Fedor Indutny, 2012.
...
```

#### <a name="apidoc.element.ip.fromPrefixLen"></a>[function <span class="apidocSignatureSpan">ip.</span>fromPrefixLen (prefixlen, family)](#apidoc.element.ip.fromPrefixLen)
- description and source-code
```javascript
fromPrefixLen = function (prefixlen, family) {
  if (prefixlen > 32) {
    family = 'ipv6';
  } else {
    family = _normalizeFamily(family);
  }

  var len = 4;
  if (family === 'ipv6') {
    len = 16;
  }
  var buff = new Buffer(len);

  for (var i = 0, n = buff.length; i < n; ++i) {
    var bits = 8;
    if (prefixlen < 8) {
      bits = prefixlen;
    }
    prefixlen -= bits;

    buff[i] = ~(0xff >> bits) & 0xff;
  }

  return ip.toString(buff);
}
```
- example usage
```shell
...
'''js
var ip = require('ip');

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true
...
```

#### <a name="apidoc.element.ip.isEqual"></a>[function <span class="apidocSignatureSpan">ip.</span>isEqual (a, b)](#apidoc.element.ip.isEqual)
- description and source-code
```javascript
isEqual = function (a, b) {
  a = ip.toBuffer(a);
  b = ip.toBuffer(b);

  // Same protocol
  if (a.length === b.length) {
    for (var i = 0; i < a.length; i++) {
      if (a[i] !== b[i]) return false;
    }
    return true;
  }

  // Swap
  if (b.length === 4) {
    var t = b;
    b = a;
    a = t;
  }

  // a - IPv4, b - IPv6
  for (var i = 0; i < 10; i++) {
    if (b[i] !== 0) return false;
  }

  var word = b.readUInt16BE(10);
  if (word !== 0 && word !== 0xffff) return false;

  for (var i = 0; i < 4; i++) {
    if (a[i] !== b[i + 12]) return false;
  }

  return true;
}
```
- example usage
```shell
...
## Usage
Get your ip address, compare ip addresses, validate ip addresses, etc.

'''js
var ip = require('ip');

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
...
```

#### <a name="apidoc.element.ip.isLoopback"></a>[function <span class="apidocSignatureSpan">ip.</span>isLoopback (addr)](#apidoc.element.ip.isLoopback)
- description and source-code
```javascript
isLoopback = function (addr) {
  return /^(::f{4}:)?127\.([0-9]{1,3})\.([0-9]{1,3})\.([0-9]{1,3})/
      .test(addr) ||
    /^fe80::1$/.test(addr) ||
    /^::1$/.test(addr) ||
    /^::$/.test(addr);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.ip.isPrivate"></a>[function <span class="apidocSignatureSpan">ip.</span>isPrivate (addr)](#apidoc.element.ip.isPrivate)
- description and source-code
```javascript
isPrivate = function (addr) {
  return /^(::f{4}:)?10\.([0-9]{1,3})\.([0-9]{1,3})\.([0-9]{1,3})$/i
      .test(addr) ||
    /^(::f{4}:)?192\.168\.([0-9]{1,3})\.([0-9]{1,3})$/i.test(addr) ||
    /^(::f{4}:)?172\.(1[6-9]|2\d|30|31)\.([0-9]{1,3})\.([0-9]{1,3})$/i
      .test(addr) ||
    /^(::f{4}:)?127\.([0-9]{1,3})\.([0-9]{1,3})\.([0-9]{1,3})$/i.test(addr) ||
    /^(::f{4}:)?169\.254\.([0-9]{1,3})\.([0-9]{1,3})$/i.test(addr) ||
    /^f[cd][0-9a-f]{2}:/i.test(addr) ||
    /^fe80:/i.test(addr) ||
    /^::1$/.test(addr) ||
    /^::$/.test(addr);
}
```
- example usage
```shell
...
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
var buf = new Buffer(128);
var offset = 64;
ip.toBuffer('127.0.0.1', buf, offset);  // [127, 0, 0, 1] at offset 64
...
```

#### <a name="apidoc.element.ip.isPublic"></a>[function <span class="apidocSignatureSpan">ip.</span>isPublic (addr)](#apidoc.element.ip.isPublic)
- description and source-code
```javascript
isPublic = function (addr) {
  return !ip.isPrivate(addr);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.ip.isV4Format"></a>[function <span class="apidocSignatureSpan">ip.</span>isV4Format (ip)](#apidoc.element.ip.isV4Format)
- description and source-code
```javascript
isV4Format = function (ip) {
  return ipv4Regex.test(ip);
}
```
- example usage
```shell
...
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
var buf = new Buffer(128);
var offset = 64;
ip.toBuffer('127.0.0.1', buf, offset);  // [127, 0, 0, 1] at offset 64
ip.toString(buf, offset, 4);            // '127.0.0.1'
...
```

#### <a name="apidoc.element.ip.isV6Format"></a>[function <span class="apidocSignatureSpan">ip.</span>isV6Format (ip)](#apidoc.element.ip.isV6Format)
- description and source-code
```javascript
isV6Format = function (ip) {
  return ipv6Regex.test(ip);
}
```
- example usage
```shell
...
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
var buf = new Buffer(128);
var offset = 64;
ip.toBuffer('127.0.0.1', buf, offset);  // [127, 0, 0, 1] at offset 64
ip.toString(buf, offset, 4);            // '127.0.0.1'
...
```

#### <a name="apidoc.element.ip.loopback"></a>[function <span class="apidocSignatureSpan">ip.</span>loopback (family)](#apidoc.element.ip.loopback)
- description and source-code
```javascript
loopback = function (family) {
  //
  // Default to 'ipv4'
  //
  family = _normalizeFamily(family);

  if (family !== 'ipv4' && family !== 'ipv6') {
    throw new Error('family must be ipv4 or ipv6');
  }

  return family === 'ipv4' ? '127.0.0.1' : 'fe80::1';
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.ip.mask"></a>[function <span class="apidocSignatureSpan">ip.</span>mask (addr, mask)](#apidoc.element.ip.mask)
- description and source-code
```javascript
mask = function (addr, mask) {
  addr = ip.toBuffer(addr);
  mask = ip.toBuffer(mask);

  var result = new Buffer(Math.max(addr.length, mask.length));

  var i = 0;
  // Same protocol - do bitwise and
  if (addr.length === mask.length) {
    for (i = 0; i < addr.length; i++) {
      result[i] = addr[i] & mask[i];
    }
  } else if (mask.length === 4) {
    // IPv6 address and IPv4 mask
    // (Mask low bits)
    for (i = 0; i < mask.length; i++) {
      result[i] = addr[addr.length - 4  + i] & mask[i];
    }
  } else {
    // IPv6 mask and IPv4 addr
    for (var i = 0; i < result.length - 6; i++) {
      result[i] = 0;
    }

    // ::ffff:ipv4
    result[10] = 0xff;
    result[11] = 0xff;
    for (i = 0; i < addr.length; i++) {
      result[i + 12] = addr[i] & mask[i + 12];
    }
    i = i + 12;
  }
  for (; i < result.length; i++)
    result[i] = 0;

  return ip.toString(result);
}
```
- example usage
```shell
...
var ip = require('ip');

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true
...
```

#### <a name="apidoc.element.ip.not"></a>[function <span class="apidocSignatureSpan">ip.</span>not (addr)](#apidoc.element.ip.not)
- description and source-code
```javascript
not = function (addr) {
  var buff = ip.toBuffer(addr);
  for (var i = 0; i < buff.length; i++) {
    buff[i] = 0xff ^ buff[i];
  }
  return ip.toString(buff);
}
```
- example usage
```shell
...
ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
var buf = new Buffer(128);
...
```

#### <a name="apidoc.element.ip.or"></a>[function <span class="apidocSignatureSpan">ip.</span>or (a, b)](#apidoc.element.ip.or)
- description and source-code
```javascript
or = function (a, b) {
  a = ip.toBuffer(a);
  b = ip.toBuffer(b);

  // same protocol
  if (a.length === b.length) {
    for (var i = 0; i < a.length; ++i) {
      a[i] |= b[i];
    }
    return ip.toString(a);

  // mixed protocols
  } else {
    var buff = a;
    var other = b;
    if (b.length > a.length) {
      buff = b;
      other = a;
    }

    var offset = buff.length - other.length;
    for (var i = offset; i < buff.length; ++i) {
      buff[i] |= other[i - offset];
    }

    return ip.toString(buff);
  }
}
```
- example usage
```shell
...
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
ip.isV4Format('127.0.0.1'); // true
ip.isV6Format('::ffff:127.0.0.1'); // true

// operate on buffers in-place
var buf = new Buffer(128);
var offset = 64;
...
```

#### <a name="apidoc.element.ip.subnet"></a>[function <span class="apidocSignatureSpan">ip.</span>subnet (addr, mask)](#apidoc.element.ip.subnet)
- description and source-code
```javascript
subnet = function (addr, mask) {
  var networkAddress = ip.toLong(ip.mask(addr, mask));

  // Calculate the mask's length.
  var maskBuffer = ip.toBuffer(mask);
  var maskLength = 0;

  for (var i = 0; i < maskBuffer.length; i++) {
    if (maskBuffer[i] === 0xff) {
      maskLength += 8;
    } else {
      var octet = maskBuffer[i] & 0xff;
      while (octet) {
        octet = (octet << 1) & 0xff;
        maskLength++;
      }
    }
  }

  var numberOfAddresses = Math.pow(2, 32 - maskLength);

  return {
    networkAddress: ip.fromLong(networkAddress),
    firstAddress: numberOfAddresses <= 2 ?
                    ip.fromLong(networkAddress) :
                    ip.fromLong(networkAddress + 1),
    lastAddress: numberOfAddresses <= 2 ?
                    ip.fromLong(networkAddress + numberOfAddresses - 1) :
                    ip.fromLong(networkAddress + numberOfAddresses - 2),
    broadcastAddress: ip.fromLong(networkAddress + numberOfAddresses - 1),
    subnetMask: mask,
    subnetMaskLength: maskLength,
    numHosts: numberOfAddresses <= 2 ?
                numberOfAddresses : numberOfAddresses - 2,
    length: numberOfAddresses,
    contains: function(other) {
      return networkAddress === ip.toLong(ip.mask(other, mask));
    }
  };
}
```
- example usage
```shell
...
// operate on buffers in-place
var buf = new Buffer(128);
var offset = 64;
ip.toBuffer('127.0.0.1', buf, offset);  // [127, 0, 0, 1] at offset 64
ip.toString(buf, offset, 4);            // '127.0.0.1'

// subnet information
ip.subnet('192.168.1.134', '255.255.255.192')
// { networkAddress: '192.168.1.128',
//   firstAddress: '192.168.1.129',
//   lastAddress: '192.168.1.190',
//   broadcastAddress: '192.168.1.191',
//   subnetMask: '255.255.255.192',
//   subnetMaskLength: 26,
//   numHosts: 62,
...
```

#### <a name="apidoc.element.ip.toBuffer"></a>[function <span class="apidocSignatureSpan">ip.</span>toBuffer (ip, buff, offset)](#apidoc.element.ip.toBuffer)
- description and source-code
```javascript
toBuffer = function (ip, buff, offset) {
  offset = ~~offset;

  var result;

  if (this.isV4Format(ip)) {
    result = buff || new Buffer(offset + 4);
    ip.split(/\./g).map(function(byte) {
      result[offset++] = parseInt(byte, 10) & 0xff;
    });
  } else if (this.isV6Format(ip)) {
    var sections = ip.split(':', 8);

    var i;
    for (i = 0; i < sections.length; i++) {
      var isv4 = this.isV4Format(sections[i]);
      var v4Buffer;

      if (isv4) {
        v4Buffer = this.toBuffer(sections[i]);
        sections[i] = v4Buffer.slice(0, 2).toString('hex');
      }

      if (v4Buffer && ++i < 8) {
        sections.splice(i, 0, v4Buffer.slice(2, 4).toString('hex'));
      }
    }

    if (sections[0] === '') {
      while (sections.length < 8) sections.unshift('0');
    } else if (sections[sections.length - 1] === '') {
      while (sections.length < 8) sections.push('0');
    } else if (sections.length < 8) {
      for (i = 0; i < sections.length && sections[i] !== ''; i++);
      var argv = [ i, 1 ];
      for (i = 9 - sections.length; i > 0; i--) {
        argv.push('0');
      }
      sections.splice.apply(sections, argv);
    }

    result = buff || new Buffer(offset + 16);
    for (i = 0; i < sections.length; i++) {
      var word = parseInt(sections[i], 16);
      result[offset++] = (word >> 8) & 0xff;
      result[offset++] = word & 0xff;
    }
  }

  if (!result) {
    throw Error('Invalid ip address: ' + ip);
  }

  return result;
}
```
- example usage
```shell
...
Get your ip address, compare ip addresses, validate ip addresses, etc.

'''js
var ip = require('ip');

ip.address() // my ip address
ip.isEqual('::1', '::0:1'); // true
ip.toBuffer('127.0.0.1') // Buffer([127, 0, 0, 1])
ip.toString(new Buffer([127, 0, 0, 1])) // 127.0.0.1
ip.fromPrefixLen(24) // 255.255.255.0
ip.mask('192.168.1.134', '255.255.255.0') // 192.168.1.0
ip.cidr('192.168.1.134/26') // 192.168.1.128
ip.not('255.255.255.0') // 0.0.0.255
ip.or('192.168.1.134', '0.0.0.255') // 192.168.1.255
ip.isPrivate('127.0.0.1') // true
...
```

#### <a name="apidoc.element.ip.toLong"></a>[function <span class="apidocSignatureSpan">ip.</span>toLong (ip)](#apidoc.element.ip.toLong)
- description and source-code
```javascript
toLong = function (ip) {
  var ipl = 0;
  ip.split('.').forEach(function(octet) {
    ipl <<= 8;
    ipl += parseInt(octet);
  });
  return(ipl >>> 0);
}
```
- example usage
```shell
...
// Same as previous.

// range checking
ip.cidrSubnet('192.168.1.134/26').contains('192.168.1.190') // true


// ipv4 long conversion
ip.toLong('127.0.0.1'); // 2130706433
ip.fromLong(2130706433); // '127.0.0.1'
'''

### License

This software is licensed under the MIT License.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
