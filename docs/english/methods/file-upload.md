# File upload

- Upload a file by local path   
  123.png -> [bucket-name]/test/07af8a67f6a4fa5f65a7f687a98fa6f2a34f.png

```javascript
var upload = await s3.Upload(
  {
    path: path.resolve(__dirname, './123.png'),
  },
  '/test/'
);

// Returns path to file in s3 and other stuff
// if it returns false - error is happened
// File is uploaded to [my-storage]/test/{md5_checksum}.{file extension}
console.log(upload); 
```

- Upload a file by local path and save filename of this file  
  123.png -> [bucket-name]/test/123.png

```javascript
var upload = await s3.Upload(
  {
    path: path.resolve(__dirname, './123.png'),
    save_name: true,
  },
  '/test/'
);

// Returns path to file in s3 and other stuff
// if it returns false - error is happened
// File is uploaded to [my-storage]/test/123.png
console.log(upload); 
```

- Upload a file by local path and assign new filename to this file in s3  
  123.png -> [bucket-name]/test/lolkek.png

```javascript
var upload = await s3.Upload(
  {
    path: path.resolve(__dirname, './123.png'),
    name: 'lolkek.png',
  },
  '/test/'
);

// Returns path to file in s3 and other stuff
// if it returns false - error is happened
// File is uploaded to [my-storage]/test/lolkek.png
console.log(upload); 
```

- Upload a buffer   
  <Buffer> -> [bucket-name]/test/cad9c7a68dca57ca6dc9a7dc8a86c.png

```javascript
var upload = await s3.Upload(
  {
    buffer: file_buffer,
  },
  '/test/'
);

// Returns path to file in s3 and other stuff
// if it returns false - error is happened
// File is uploaded to [my-storage]/test/{md5_checksum}.{file extension}
console.log(upload); 
```

- Upload a buffer with filename and extension  
  <Buffer> -> [bucket-name]/test/lolkek.png

```javascript
var upload = await s3.Upload(
  {
    buffer: file_buffer,
    name: 'lolkek.png',
  },
  '/test/'
);

// Returns path to file in s3 and other stuff
// if it returns false - error is happened
// File is uploaded to [my-storage]/test/lolkek.png
console.log(upload); 
```

Example of successful response:

```javascript
{
  ETag: '"md5sum"',
  VersionId: 'null',
  Location:
   'https://actid-storage.storage.yandexcloud.net/test1/name.png',
  key: 'test/123.png',
  Key: 'test/123.png',
  Bucket: 'storage-name'
}
```