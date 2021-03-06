# Strophe http-file-upload

Plugin for [strophe.js](https://www.npmjs.com/package/strophe.js) to provide HTTP File Upload ([XEP-0363]( http://xmpp.org/extensions/xep-0363.html)).

## Install

This is a [Node.js](https://nodejs.org/en/) module available through the
[npm registry](https://www.npmjs.com/). Installation is done using the
[`npm install` command](https://docs.npmjs.com/getting-started/installing-npm-packages-locally):

```sh
$ npm install strophejs-plugin-http-file-upload
```

## Initialization

`connection.httpUpload.init(connection);`

## Usage

### Generate GET and PUT URL for file

`connection.httpUpload.getUrls(file, success_cb, error_cb)`

`file` is the File object which you want to upload.

`success_cb` is a function to be called on success with urls:

`error_cb` is a function to be called in case of error. 

Function will return object with put and get url. You can use put url to upload file using http.


### Example

Generate get and put url for file:

    var file = {
        name: 'filename.png',
        size: 4512, // in bytes
        type: 'image/png',
        ... // other data
    }
    
    function uploadFile(file, url) {
        var xhr = new XMLHttpRequest();
    
        xhr.onreadystatechange = function() {
            if (xhr.readyState === 4) {
                console.log('File Uploaded Successfully.');
            }
        };
    
        xhr.open("PUT", url, true);
        xhr.setRequestHeader('Content-Type', 'text/plain');
        xhr.send(file);
    }

    connection.httpUpload.getUrls(
        file,
        function(data) {
            console.log("PUT URL: ", data.put, "GET URL: ", data.get);
            uploadFile(file, data.put);
            return true;
        },
        function(err) {
            console.error(err);
        }
    );

## License

strophejs-plugin-http-file-upload is copyright (c) 2019-present Anish Lushte <lushteanish@gmail.com> and
the [contributors to Node-Minio](https://github.com/anishlushte07/strophejs-plugin-http-file-upload/graphs/contributors).

strophejs-plugin-http-file-upload is free software, licensed under the MIT License. See the
`LICENSE` file for more details.

