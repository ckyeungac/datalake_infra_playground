# Background

This creates the playground for a modern data lake infrastructure.

- Data Storage: MinIO
- Data Query Engine: Dremio
- Data Lake Engine: Spark + Iceberg
- [Todo] Data Visualization: Metabase

To start-up the infrastructure, run 

```
docker-compose up
```

Once the containers are up and running, we can access

- Jupyter Notebook: http://localhost:8888
- Spark Driver UI: http://localhost:8080
- Spark History UI: http://localhost:18080
- MinIO UI: http://localhost:9001
- Dremio UI: http://localhost:9047


## Adding MinIO in Dremio
1. Click `Add Source`
2. Choose `Amazon S3`
3. Put the following configuration
   1. Inside General
      1. Name: `MinIO`
      2. Authentication: `AWS Access Key`
         1. AWS Access Key: `admin`
         2. AWS Access Secret: `password`
         3. IAM Role to Assume: <LEAVE BLANK>
   2. Inside Advanced Options
      1. Check the following
         1. Enable asynchronous access when possible
         2. Enable compatibility mode
         3. Enable file status check
         4. Enable partition column inference
      2. Under Connection Properties, set the following key-value pairs
         1. `fs.s3a.path.style.access`: `true`
         2. `fs.s3a.endpoint:http`: `http://minio:9000`
         3. `fs.s3a.connection.ssl`: `false`
4. Click "Save".

