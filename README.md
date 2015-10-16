# injectr # [![Build Status](https://travis-ci.org/nathanmacinnes/injectr.svg?branch=master)](https://travis-ci.org/nathanmacinnes/injectr)

_Finally, a solution to node.js dependency injection_

## Install it ##

`npm install injectr`. Boom.

## Use it ##

    var injectr = require('injectr');
    var myScript = injectr('../lib/myScript.js', {
        fs : mockFs,
        crypto : mockCrypto
    });

Now when you `require('fs')` or `require('crypto')` in myScript.js, what you
get is `mockFs` or `mockCrypto`.

Treat **injectr** like `require` for your tests, with a second argument to pass
in your mocks.

**Paths are now relative to the current file, just like require.** Please update
your tests if you are upgrading from v0.4 or below.

### Context ###

**injectr** gives you access to the context of the **injectr**'d file via
an optional third argument. Provide an object, and **injectr** will modify it
as necessary and use that as the context.

    var myScript = injectr('../lib/myScript.js', {}, {
        Date : mockDate,
        setTimeout : mockSetTimeout
    });

As of version 0.4, **injectr** doesn't create a full node.js context for you to
use. Instead, it isolates your script in its own sandbox, allowing you to
include mocks of only the bits that your script needs.

### CoffeeScript ###

**injectr** compiles any *.coffee files for you, so you can test your
CoffeeScript too. The default settings can be changed by overwriting the
`injectr.onload` function. It takes the filename and file contents as
arguments, and returns the compiled script.

## Share it ##

**injectr** is under the [MIT License](http://www.opensource.org/licenses/MIT).
[Fork it](https://github.com/nathanmacinnes/injectr). Modify it. Pass it around.
