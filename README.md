## CKAN Helm Chart

This is a fork of the [CKAN Helm Chart](https://github.com/ckan/ckan-helm) with some modifications to support Tapis OAuth.

### Manage users

To manage users, you can use the [CKAN API](https://docs.ckan.org/en/2.9/api/index.html).

```bash
ckan -c production.ini sysadmin add john_doe
```

### S3 Integration

```
# Set this parameter only if you want to use Minio as a filestore service instead of S3.
ckanext.s3filestore.host_name = http://minio-service.com
# Don't check for access on each startup
ckanext.s3filestore.check_access_on_startup = false
# The bucket name to store your stuff
ckanext.s3filestore.aws_bucket_name = a-bucket-to-store-your-stuff
# Region name
ckanext.s3filestore.region_name= region-name
# Signature version
ckanext.s3filestore.signature_version = s3v4
# Access key ID
ckanext.s3filestore.aws_access_key_id = Your-Access-Key-ID
# Secret access key
ckanext.s3filestore.aws_secret_access_key = Your-Secret-Access-Key
```

# Conditional:

```
# An optional setting to fallback to filesystem for downloads
ckanext.s3filestore.filesystem_download_fallback = true
# The ckan storage path option must also be set correctly for the fallback to work
ckan.storage_path = path/to/storage/directory

# An optional setting to change the acl of the uploaded files. Default public-read.
ckanext.s3filestore.acl = private

# An optional setting to specify which addressing style to use. This controls whether the bucket name is in the hostname or is part of the URL. Default auto.
ckanext.s3filestore.addressing_style = path

# To mask the S3 endpoint with your own domain/endpoint when serving URLs to end users.
# This endpoint should be capable of serving S3 objects as if it were an actual bucket.
# The real S3 endpoint will still be used for uploading files.
ckanext.s3filestore.download_proxy = https://example.com/my-bucket

# Defines how long a signed URL is valid (default 1 hour).
ckanext.s3filestore.signed_url_expiry = 3600

```

## S3 Secrets

The S3 secrets are stored in a Kubernetes secret. The secret should have the following keys:

- `aws-access-key-id`
- `aws-secret-access-key`

```bash
kubectl create secret generic ckan-s3-secrets \
  --from-literal=aws-access-key-id='Your-Access-Key-ID' \
  --from-literal=aws-secret-access-key='Your-Secret-Access-Key'
```
