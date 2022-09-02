# Clean up

Clean up bucket

```javascript
const result = await s3.CleanUp();
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