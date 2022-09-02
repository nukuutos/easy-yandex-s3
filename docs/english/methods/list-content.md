# List content

- Get root of the bucket

```javascript
var list = await s3.GetList();
```

- Getting a list of subfolder and files of specific directory

```javascript
var list = await s3.GetList('/test');
```

- `Contents` - contains files that are in folder `test`
- `CommonPrefixes` - contains subfolders that are in folder `test`

**return:**

```javascript
{
  IsTruncated: false,
  Contents: [
    {
      Key: 'eys3-testing/file1.rtf',
      LastModified: new Date("2022-08-24T01:55:02.431Z"),
      ETag: '"ee4e1fb1ab82ee0a650d8e4a8c274d9b"',
      ChecksumAlgorithm: [],
      Size: 413,
      StorageClass: 'STANDARD',
      Owner: [Object]
    },
    {
      Key: 'eys3-testing/file2.rtf',
      LastModified: new Date("2022-08-24T01:55:02.483Z"),
      ETag: '"ee4e1fb1ab82ee0a650d8e4a8c274d9b"',
      ChecksumAlgorithm: [],
      Size: 413,
      StorageClass: 'STANDARD',
      Owner: [Object]
    }
  ],
  Name: 's3library',
  Prefix: 'eys3-testing/',
  Delimiter: '/',
  MaxKeys: 1000,
  CommonPrefixes: [ { Prefix: 'eys3-testing/folder1/' } ],
  KeyCount: 3
}
```