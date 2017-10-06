#htmlparser-benchmark

> Simple benchmark for diffrent htmlparsers using real-life data

## Installation

```shell
npm install htmlparser-benchmark
```

## How to run

#### Use as a module

```javascript
var benchmark = require('htmlparser-benchmark');
var Parser = require("htmlparser2").Parser;

var bench = benchmark(function (html, callback) {
	var parser = new Parser({
		onend: callback,
		onerror: callback
	});
	parser.end(html);
});

bench.on('progress', function (key) {
	console.log('finished parsing ' + key + '.html');
});

bench.on('result', function (stat) {
	console.log(stat.mean().toPrecision(6) + ' ms/file ± ' + stat.sd().toPrecision(6));
});
```

Where `stat` is a [Summary](https://github.com/AndreasMadsen/summary) object.

#### Use the script

You can also just run `npm test`, that will benchmark all the modules listed
in the `wrapper` directory. Note that you will need to install the `dev-dependencies`
first.

```shell
cd htmlparser-benchmark
npm install
npm test
```

### Results

Tested on a Mid 2015 Macbook Pro, 2.5 GHz Intel Core i7, running node 8.6.0 and npm 4.6.1.

Both `jsdom-fragment` and `jsdom-node-locations` threw errors on tests 84, 89, 103, 111,
and 137 with the initial message (or some variant of):

> Could not parse CSS @import URL ... relative to base URL "about:blank"

So tests for them may not be 100% accurate, but close enough for me. Additionally, a few
other parsers failed altogether. 

      gumbo-parser        : 25.2510 ms/file ± 13.1904
      high5 failed          (exit code 1)
      html-parser         : 27.1866 ms/file ± 21.4137
      html5               : 178.019 ms/file ± 232.016
      htmlparser          : 14.1844 ms/file ± 79.8066
      htmlparser2-dom     : 6.13265 ms/file ± 5.81879
      htmlparser2         : 4.36647 ms/file ± 4.50375
      hubbub failed         (exit code 1)
    * jsdom-fragment      : 37.3501 ms/file ± 22.5679
    * jsdom-node-locations: 115.443 ms/file ± 62.5155
    * jsdom               : 48.1934 ms/file ± 26.5845
      libxmljs            : 4.63207 ms/file ± 4.72320
      neutron-html5parser : 3.18836 ms/file ± 1.90246
      parse5 failed         (exit code 1)
      sax                 : 10.0947 ms/file ± 13.6911

Same list, but sorted:

      high5 failed          (exit code 1)
      hubbub failed         (exit code 1)
      parse5 failed         (exit code 1)
      neutron-html5parser : 3.18836 ms/file ± 1.90246
      htmlparser2         : 4.36647 ms/file ± 4.50375
      libxmljs            : 4.63207 ms/file ± 4.72320
      htmlparser2-dom     : 6.13265 ms/file ± 5.81879
      sax                 : 10.0947 ms/file ± 13.6911
      htmlparser          : 14.1844 ms/file ± 79.8066
      gumbo-parser        : 25.2510 ms/file ± 13.1904
      html-parser         : 27.1866 ms/file ± 21.4137
    * jsdom-fragment      : 37.3501 ms/file ± 22.5679
    * jsdom               : 48.1934 ms/file ± 26.5845
    * jsdom-node-locations: 115.443 ms/file ± 62.5155
      html5               : 178.019 ms/file ± 232.016

## License

**The software is license under "MIT"**

> Copyright (c) 2013 Andreas Madsen
>
> Permission is hereby granted, free of charge, to any person obtaining a copy
> of this software and associated documentation files (the "Software"), to deal
> in the Software without restriction, including without limitation the rights
> to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
> copies of the Software, and to permit persons to whom the Software is
> furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in
> all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
> IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
> FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
> AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
> LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
> OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
> THE SOFTWARE.
