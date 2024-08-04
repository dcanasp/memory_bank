# S3
The file storage system, it's pretty simple. Have any image, file, zip, or anything, just turn it to [[binary]] and upload it, you can have different folders

You can also store code on S3, and execute it with a [[high level/cloud/aws/Compute#Lambda|Lambda]]

>[!info]
>Buckets name MUST be unique on all regions, but the exist only in one  region, (this is because s3 gives you a public [[url]] where you can see your bucket)

To start just create the bucket, after doing it. manage who can use it. This is done with buckets policies. Bucket policy for 

example for an all entries (insert, read, delete) policy:
it's important to note that this should NOT be done on production, on production you set only an [[IP]] to create (your [[server]])
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        },
        {
            "Sid": "AllowPublicWrite",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:PutObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}

```
and for all the cors:
```json
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "POST",
            "PUT",
            "DELETE",
            "HEAD"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [
            "ETag",
            "x-amz-meta-custom-header"
        ],
        "MaxAgeSeconds": 3000
    }
]

```
# EBS
Elastic Block Storage is the storage service that [[high level/cloud/aws/Compute#EC2|EC2]] uses, it's the [[Physical memory]] of a virtual machine, They can be HDD or SDD. The key feature is being able to take snapshots as backups for a EC2 instance, and the encryption by default of the data.

EBS can only be used when attached to an [[high level/cloud/aws/Compute#EC2|EC2]]
