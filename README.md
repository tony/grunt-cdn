[Grunt][grunt] plugin for properly prepending a CDN url to those assets referenced with absolute paths (but not URLs)

## Getting Started

Install this grunt plugin next to your project's gruntfile with: `npm install grunt-cdn`

Then add this line to your project's `grunt.js` gruntfile:

```javascript
grunt.loadNpmTasks('grunt-cdn');
```

Then specify your config:

```javascript
    grunt.initConfig({
        cdn: {
            dist: {
                /** @required  - string (or array of) including grunt glob variables */
                src: ['./static/*.html', './static/*.css', './static/*.soy'],
                /** @optional  - if provided a copy will be stored without modifying original file */
                dest: './dist/static/',
                /** @required - root URL of your CDN (may contains sub-paths as shown below) */
                cdn: 'http://cdn.cloudfront.net/container/'
            }
        }
    });
```

### Example

With the following input

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mural.ly</title>
    <link rel="stylesheet" type="text/css" href="/static/compiled.css?v=13512tyu3kds" />
</head>
<body id="landing-page">
...
</body>
</html>
```

After running the task the output looks like

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mural.ly</title>
    <link rel="stylesheet" type="text/css" href="http://cdn.cloudfront.net/container/static/compiled.css?v=13512tyu3kds" />
</head>
<body id="landing-page">
...
</body>
</html>
```

As you can see we maintain the "container" pathname in this case, and we also keep the original
query strings. This task is really handy if you upload stuff from your CI to make it transparent
to developers.

**NOTE**: This task only works with "absolute" paths. We consider paths starting with
. (or ..) as relative, and with / absolute. We're using the same aproach as the *NIX file-system.

## Release History
* 0.1.0 Initial Release

[grunt]: https://github.com/cowboy/grunt
