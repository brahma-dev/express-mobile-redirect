# Mobile/Tablet Redirection for Node.js and Express

Express middleware to detect if the request came from a mobile/tablet browser and optionally redirect accordingly.

## Usage

```javascript
var express = require('express');
var ua  = require('express-mobile-redirect');

/* Desktop */
var app = express();
app.use(ua.mobileredirect('http://localhost:3001')); // Detects mobiles and sets req.is_mobile and redirects
app.use(ua.tabletredirect('http://localhost:3001')); // Detects tablets and sets req.is_tablet and redirects
app.get('/', function(req, res) {
    return res.json({
        desktopsite: true,
        is_mobile: req.is_mobile,
        is_tablet: req.is_tablet
    });
});
app.listen(3000);

/* Mobile */
var app2 = express();
app2.use(ua.is_mobile()); // Detects mobiles and sets req.is_mobile
app2.use(ua.is_tablet()); // Detects tablets and sets req.is_tablet
app2.get('/', function(req, res) {
    if (!req.is_mobile && !req.is_tablet) {
        return res.redirect('http://localhost:3000');
    }
    return res.json({
        mobilesite: true,
        is_mobile: req.is_mobile,
        is_tablet: req.is_tablet
    });
});
app2.listen(3001);
```

## Credit

Regex based from http://detectmobilebrowsers.com and other bits and pieces from the internet.


## LICENSE
(The MIT License)

Copyright (c) 2015 afzaalace

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
