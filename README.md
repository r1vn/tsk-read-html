parses JSON+HTML source files

```
---
{
    "title": "Hello world",
    "date": "2021-01-01 12:34"
}
---
<h1>Hello, world</h1>
<p>lorem ipsum dolor ...
```
->
```
{
    path: 'index.source.html',
    data: {
        title: 'Hello world',
        date: '2021-01-01 12:34'
    },
    html: '<h1>Hello, world</h1><p>lorem ipsum dolor ...'
}
```

## setup

- download [tsk-read-html.tar.xz](https://github.com/r1vn/tsk-read-html/raw/master/tsk-read-html.tar.xz) and unpack as `your-project/lib/tsk-read-html`
- add a config entry to the manifest

example config: parsing all .source.html files from `source` into `tmp/sources.json`

```
{
    module: 'lib/tsk-read-html',
    config:
    {
        // path of the directory to get files from
        sourceDir: 'source',
        // filter for the files in sourceDir
        filterFn: srcPath => srcPath.endsWith('.source.html'),
        // JSON output file path
        outputFile: 'tmp/sources.json',
        // if set to false, entries will be appended to the existing output file instead of overwriting it
        overwrite: true,
        // toggles verbose output
        verbose: true
    }
}
```

input:

```
source/foo/index.source.html
source/bar/index.source.html
source/about.source.html
source/contact.source.html
source/index.source.html
```

output:

`tmp/sources.json`
```
[
    {
        "path": "source/foo/index.source.html",
        "data": { ... },
        "html": "..."
    },
    {
        "path": "source/bar/index.source.html",
        "data": { ... },
        "html": "..."
    },
    {
        "path": "source/about.source.html",
        "data": { ... },
        "html": "..."
    },
    {
        "path": "source/contact.source.html",
        "data": { ... },
        "html": "..."
    },
    {
        "path": "source/index.source.html",
        "data": { ... },
        "html": "..."
    }
]
```