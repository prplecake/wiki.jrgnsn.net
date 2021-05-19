---
title: Pleroma - Setting up Object Storage
---

I used Minio for my object storage server, but these instructions should be adaptable to any object storage server that implements the AWS S3 API.

This guide assumes you already have a working object storage server, and you have the Minio client installed. We also assume you've already created a user and bucket for Pleroma.

# Bucket Configuration

The bucket that Pleroma will use for object storage need to allow anonymous fetch. In Minio, this is configured with a bucket policy.

I'm using _fetchonly.json_ from <https://gist.github.com/CosmicToast/a53e6276cf60e8f40ad6650dc3abb0ae>. Save it to a file then run:
```
mc policy set-json /path/to/fetchonly.json myminio/bucket-name
```

# Pleroma Configuration

Your Pleroma configuration should include something like the following:

```elixir
config :pleroma, Pleroma.Upload,
  uploader: Pleroma.Uploaders.S3

config :pleroma, Pleroma.Uploaders.S3,
  bucket: "your-bucket",
  public_endpoint: "https://minio.example.com"

# Configure S3 credentials:
config :ex_aws, :s3,
  access_key_id: "your-access-key",
  secret_access_key: "your-access-secret",
  scheme: "https://"

# For using third-party S3 clones like wasabi, also do:
config :ex_aws, :s3,
  host: "minio.example.com"
```

**Note:** As far as I know, it's not possible to configure object storage with Pleroma admin-fe.

# See also
* [[Minio user policy|/Self_Hosting/Pleroma/Minio_user_policy]]
