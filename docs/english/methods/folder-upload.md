# Folder upload

- Upload content of a local folder -> [bucket]/folder_on_server/

Our module takes files and subfolders inside local folder.

Suppose a folder `./my_folder`:

- my_folder
- - 1.png
- - 2.png
- - folder_inside
- - - 3.png

Set `route` parameter to "**folder_on_server**", and we get this path on s3 `[my_bucket]/folder_on_server/`  
Our files after uploading to s3:

`[my_bucket]/folder_on_server/1.png `
`[my_bucket]/folder_on_server/2.png `
`[my_bucket]/folder_on_server/folder_inside/3.png `

```javascript
// Relative path:
var upload = await s3.Upload(
  {
    path: './my_folder', // relative path to folder
    save_name: true, // save original names of files
  },
  '/folder_on_server/'
);
console.log(upload); // <- array of uploaded files
```

```javascript
// Ignore files and folders inside
var upload = await s3.Upload(
  {
    path: './my_folder', // relative path to folder
    save_name: true, // save original names of files
    ignore: ['.git', '/assets/video'], // ignore .git and path /assets/video
  },
  '/folder_on_server/'
);
console.log(upload); // <- array of uploaded files
```

```javascript
// absolute path to local file:
var upload = await s3.Upload(
  {
    path: '/Users/powerdot/sites/example.com/', // absolute path to folder
    save_name: true, // save original names of files
  },
  '/folder_on_server/'
);
console.log(upload); // <- array of uploaded files
```