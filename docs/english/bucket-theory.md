# About Yandex.Cloud buckets

The storage consists of buckets. Bucket is your hard drive on the Internet. To upload something to Yandex.Cloud and store your files there, you need to create this bucket.

- Bucket has `name`, which you come up with, for example `storage-name`.
- Bucket access can be obtained using a special account, it is called `service account`.
- Service account can have a `key`. There's three types of key, but we need `static access key` to use S3. Key has `ID` and `secret key`.

We suppose that you have already created bucket. We have a guid to [create a service account and obtain static access key](service-account-and-static-access-key.md). 