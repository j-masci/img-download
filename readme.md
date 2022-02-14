Copy and paste into your browser console to trigger a download of all images found in the markup.

```js

var imgdl = {
    regex: /(http)?s?:?(\/\/[^"']*\.(?:png|jpg|jpeg|gif|svg))/gi,
    filenameRegex: /(?:.+\/)(.+)/,    
    getTargetStr: function(){ return document.getElementsByTagName('body')[0].innerHTML; },
    getUrls: function() {
        return this.getTargetStr().match(this.regex);
    },
    getFilename: function( url ) {
        return url.match(this.filenameRegex)[1];
    },
    download: function( urls ) {

        var anchor;

        // wow vanilla js is painful.
        for (var i = 0; i < urls.length; i++) {
            anchor = document.createElement('a');
            anchor.href = urls[i];
            anchor.target = "_blank";
            anchor.download = this.getFilename(urls[i]);
            document.documentElement.append(anchor);
            anchor.click();
            anchor.remove();
        }
    }
}

imgdl.download(imgdl.getUrls());

```