# Upload files

```javascript
// using an array of files:
var upload = await s3.Upload(
  [
    { path: './file1.jpg', save_name: true }, // relative path to file, save name of this file
    { path: '/Users/powerdot/dev/sites/folder/file2.css' }, // absolute path to file, filename will be updated to md5-checksum
    { path: './file.html', name: 'index.html' }, // relative path to file with new name index.html
  ],
  '/folder_on_server/'
);
```

**return:**  
Array with uploaded objects

```javascript
[
    {
        ETag: '"md5sum"',
        VersionId: 'null',
        Location:
            'https://actid-storage.storage.yandexcloud.net/test1/name.png',
        key: 'test1/name.png',
        Key: 'test1/name.png',
        Bucket: 'actid-storage'
    },
    ...
]
```