[![Easy Yandex S3 Logo](https://storage.yandexcloud.net/actid-storage/easy-yandex-s3/eys3.png)](https://github.com/powerdot/easy-yandex-s3)

[![Build Status](https://travis-ci.org/powerdot/easy-yandex-s3.svg?branch=master)](https://travis-ci.org/powerdot/easy-yandex-s3) [![YouTube IlyaDevman](https://storage.yandexcloud.net/actid-storage/GitHubImages/gt-yt-overview.png)](https://youtu.be/L_6PiJFaldI)

Using the S3 API **_Yandex.Cloud_** is even easier.
The storage is called **_Object Storage_**.

Support from Node.js 8 version

✓ Upload a file  
✓ Upload an array of files  
✓ Upload entire folders with nested folders and files inside  
✓ Upload a Buffer  
✓ Download files from bucket  
✓ Delete individual files from a bucket  
✓ Clean up bucket  
✓ Get information about files in a bucket

Let's go!

## Contents

- [Instruction](#introduction)
- [Get started](#get-started)
- [File upload](#file-upload)
- [Folder upload](#folder-upload)
- [Upload files](#upload-files)
- [List content](#list-content)
- [Download a file](#download-a-file)
- [Remove a file](#remove-a-file)
- [Remove every file](#remove-every-file-from-bucket)
- [Examples](#examples)
- - [Upload with multer](#multer-and-express)

Links:  
- [Official Yandex docs](https://cloud.yandex.ru/docs/storage/s3)  
- [Description of S3 API Amazon](https://docs.aws.amazon.com/en_us/AmazonS3/latest/API/Welcome.html)

Developers:
- [@powerdot](https://github.com/powerdot/)
- [@nukuutos](https://github.com/nukuutos/)


## Introduction

You can read [theory](bucket-theory.md) about working with bucket and guid to [create a service account and obtain static access key](service-account-and-static-access-key.md). For working with this package you need `accessKeyId` and `secretAccessKey` that you get after creating a `static access key`


## Get Started

Install it with npm

```bash
npm i --save easy-yandex-s3
```

### Initialization stage

```javascript
const EasyYandexS3 = require('easy-yandex-s3');

const s3 = new EasyYandexS3({
  auth: {
    accessKeyId: 'KEY_ID',
    secretAccessKey: 'SECRET_KEY',
  },
  Bucket: 'BUCKET_NAME',
  debug: true, // debug by output in console
});
```

## File upload

Upload a file to s3 bucket.

General usage:

```javascript
s3.Upload(parameters, folderPathS3)
```

`parameters` object has next fields:
- `name` - set new name to file on s3 bucket.
- `path` - path to local file that you want to upload. 
- `save_name` - allows to save name of file that you want to upload. By default we assign to file a uuid as filename on s3 bucket. 
- `buffer` - buffer object that you want to upload.

Providing `buffer` or `path` is required!

`folderPathS3` - path to folder on bucket.

Example of file uploading to `test` folder on bucket with path and new filename
```javascript
const result = await s3.Upload(
  {
    path: './123.png',
    name: 'new-filename.png',
  },
  '/test'
);
```

[More examples of file uploading](./methods/file-upload.md)

## Folder upload

Upload only <ins>**content**</ins> of a local folder!

```javascript
s3.Upload(parameters, folderPathS3)
```

`parameters` object has next fields:
- `path` - path to the folder whose contents you want to upload. 
- `save_name` - allows to save original filenames. By default we assign to file a uuid as filename on s3 bucket. 
- `ignore` - array of files and directories that you want to ignore.

`folderPathS3` - path to folder on bucket.

Example of uploading content of `my-folder` to `test` folder on bucket. We save filenames and ignore `file.txt` file and ignore `/assets/video` directory 

```javascript
const result = await s3.Upload(
  {
    path: './my-folder',
    save_name: true, 
    ignore: ['file.txt', '/assets/video']
  },
  '/test'
);
```

[More examples of folder uploading](./methods/folder-upload.md)

## Upload files

Upload an array of files 

```javascript
s3.Upload(files, folderPathS3)
```

`files` is an array of file-objects with the following properties:
- `name` - set new name to file on s3 bucket.
- `path` - path to local file that you want to upload. 
- `save_name` - allows to save name of file that you want to upload. By default we assign to file a uuid as filename on s3 bucket. 
- `buffer` - buffer object that you want to upload.

Providing `buffer` or `path` for file-object is required!

Example of uploading array of files. Upload files to `test` folder on s3
```javascript
const result = await s3.Upload(
  [
    { path: './file1.jpg', save_name: true }, 
    { path: '/Users/powerdot/dev/sites/folder/file2.css' },
    { path: './file.html', name: 'index.html' },
  ],
  '/test'
);
```

[More examples of folder uploading](./methods/upload-files.md)

## List content

List content that is in a specific directory

General usage:

```javascript
s3.GetList(path);
```

`path` - path to directory content(file and folders) whose you want to list 

Example of listing files and subfolder in `test` directory

```javascript
const { Contents, CommonPrefixes } = await s3.GetList('/test');
```

- `Contents` is an array that contains files that are in folder `test`
- `CommonPrefixes` is an array that contains subfolders that are in folder `test`

[More examples of listing content](./methods/list-content.md)


## Download a file

Download a file from bucket

General usage:

```javascript
s3.Download(
    filepathS3,
    pathToDownload
);
```

- `filepathS3` - path to file on s3.  
- `pathToDownload` - path for saving on your machine.

`pathToDownload` is optional argument. When you download a file from the bucket you always receive a buffer of this file.   

Example of downloading file and saving it.

```javascript
const result = await s3.Download('test/bucket-file.png', './my-file.png');
```
`result.data.Body` - has a buffer of `bucket-file.png`

[More examples of downloading file](./methods/download-file.md)


### Remove a file

General usage:

```javascript
.Remove(
    "/path/to/file/in/bucket"
);
```

- Remove a file

```javascript
var remove = await s3.Remove('test/123.png');

// Returns true или false.
// true - file is removed successfully, even if the file does not exist
// false - error
```

**return:**

```javascript
true;
```

### Remove every file from bucket

General usage:

```javascript
.CleanUp()
```

Clean up bucket:

```javascript
var result = await s3.CleanUp();
```

Technically, files are deleted in batches by 1000 files. Each batch will have its own `Deleted` and `Errors` keys, which contain data about successfully deleted objects (files) and data about files that caused an error to be deleted. <br />
**return:**

```javascript
// Successfully deleted 3 objects
[ { Deleted: [ [Object], [Object], [Object] ], Errors: [] } ]

// What is object in side
{ Key: '/path/to/file/in/bucket', VersionId: 'null' }

// On unsuccessfully running of 'CleanUp' method you've got next result:
false
```

## Examples

### Multer and Express

An example of uploading files via multer and express.
Case: you need to upload a file from the client to the server, and then upload it to Yandex Object Storage.

- Installing express and multer

```bash
npm i express
npm i multer
```

- Importing multer and easy-yandex-s3

```javascript
// Creating a web server
var express = require('express');
var app = express();
app.listen(8000);

// Importing multer и eys3
var multer = require('multer');
var EasyYandexS3 = require('easy-yandex-s3');

// Setting up s3 object
var s3 = new EasyYandexS3({
  auth: {
    accessKeyId: '',
    secretAccessKey: '',
  },
  Bucket: 'my-storage', 
  debug: false, 
});

// Running multer middleware for uploading files
app.use(multer().any());

// Making a post request with file be route /uploadFile
app.post('/uploadFile', async (req, res) => {
  let buffer = req.files[0].buffer; // Buffer of uploaded file
  var upload = await s3.Upload({ buffer }, '/files/'); // Upload to bucket
  res.send(upload); // Sever responds with response from Yandex Object Storage
});
```
