# Download a file

- Download file and get buffer of this file

```javascript
var download = await s3.Download('test/123.png');
```

- Download file and save it to local file

```javascript
var download = await s3.Download('test/123.png', './myfile.png');

// download variable also has a buffer of downloaded file
// received file from bucket will be saved as myfile.png
```

**return:**

```javascript
{
  data: {
    AcceptRanges: "bytes",
    LastModified: new Date("2019-07-15T22:10:09.000Z"),
    ContentLength: 20705,
    ETag: '"md5sum"',
    ContentType: "application/octet-stream",
    Metadata: {},
    Body: Buffer.from("250001000192CD0000002F6D6E742F72", "hex"),
  },
  destinationFullPath: false,
  fileReplaced: false,
};
```