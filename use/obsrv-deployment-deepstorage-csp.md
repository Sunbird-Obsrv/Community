**Druid:**
|  	| Key 	| Value 	| Description 	|
|---	|---	|---	|---	|
| AWS 	| druid_deepstorage_type 	| S3 	| Deepstorage type where the needs to be pushed. 	|
| AWS	| s3_access_key 	| "" 	| Access key to access the bucket. 	|
| AWS 	| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
| AWS 	| druid_indexer_logs_prefix 	| "backups/druid/druid-task-logs" 	| Path inside the bucket where we wanted to store indexer logs. 	|
| AWS 	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored.  	|
| MinIO 	| druid_deepstorage_type 	| S3 	| Deepstorage type where the needs to be pushed. 	|
| MinIO 	| druid_s3_endpoint_url 	| http://172.20.126.232:9000/ 	| Minio service endpoint url to enable druid use MinIO as deepstorage. 	|
| MinIO	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|
| MinIO 	| s3_access_key 	| "" 	| Access key to access the bucket. 	|
| MinIO 	| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
| MinIO 	| s3_bucket 	| "druid-bucket" 	| Deepstorage container name. 	|
| MinIO 	| druid_s3_endpoint_signingRegion 	| "us-east-2" 	| Region where the deepstorage container created. 	|
| MinIO 	| druid_indexer_logs_directory 	| "backups/druid/druid-task-logs" 	| Path inside the bucket where we wanted to store indexer logs. 	|
| AZURE 	| azure_storage_account_name 	| "druid-blob" 	| Deepstorage container name. 	|
| AZURE 	| azure_storage_account_key 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|
| AZURE 	| druid_storage_directory 	| "/data" 	| Root path inside the blob storage where all the druid data is pushed. 	|
| GCP 	| gcs_bucket 	| "druid-bucket" 	| Deepstorage container name. 	|
| GCP 	| google_application_credentials 	| "" 	| Google cloud credentials json file where the access_token and credentials are stored. 	|
| GCP 	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|

**Flink:**
| Key 	| Value 	| Description 	|
|---	|---	|---	|
| checkpoint_store_type 	| S3 	| Type of the deepstorage container. 	|
| s3_access_key 	| "" 	| Access key to access the bucket. 	|
| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
| base.url 	| "s3://flink-bucket" 	| Deepstorage container name. 	|
| checkpoint_store_type 	| S3 	| Type of the deepstorage. 	|
| s3_access_key 	| "" 	| Access key to access the bucket. 	|
| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
| s3_endpoint 	| "http://172.20.126.232:9000" 	| Minio service endpoint url  to enable flink use MinIO as deepstorage. 	|
| base.url 	| "s3://flink-bucket" 	| Deepstorage container url. 	|
| checkpoint_store_type 	| "Blob" 	| Type of the deepstorage container. 	|
| azure_account 	| "" 	| Account key to access the blob storage. 	|
| azure_secret 	| "" 	| Secret key to access the blob. 	|
| base.url 	| "blob://flink-bucket" 	| Deepstorage container url. 	|
| checkpoint_store_type 	| "gcp" 	| Type of the deepstorage container. 	|
| google_service_account_key_path 	| "/data/flink/gcp_cred.conf" 	| Configmap path where google credentials are stored and mounted.The credential path needs to exposed as environment variable. 	|

**Secor:**

|  	| Key 	| Value 	| Description 	|
|---	|---	|---	|---	|
| AWS 	| upload_manager 	| "com.pinterest.secor.uploader.S3UploadManager" 	| s3 upload manager which is responsible to upload backup to deepstorage. 	|
|  	| cloud_store_provider 	| "S3" 	| Type of the deepstorage. 	|
|  	| aws_access_key 	| "" 	| Access key to access the bucket. 	|
|  	| aws_secret_key 	| "" 	| Secret key to access the bucket. 	|
|  	| aws_endpoint 	| https://secor-bucket.s3.us-east-2.amazonaws.com/ 	| Bucket endpoint url where all the secor backups are pushed. 	|
|  	| secor_s3_bucket 	| "secor-bucket" 	| Deepstorage container name. 	|
|  	| aws_region 	| "us-east-2" 	| Deepstorage container region. 	|
| MinIO 	| upload_manager 	| "com.pinterest.secor.uploader.S3UploadManager" 	| s3 upload manager which is responsible to upload backup to deepstorage. 	|
|  	| cloud_store_provider 	| "S3" 	| Type of the deepstorage. 	|
|  	| aws_access_key 	| "" 	| Access key to access the bucket. 	|
|  	| aws_secret_key 	| "" 	| Secret key to access the bucket. 	|
|  	| aws_endpoint 	| http://172.20.126.232:9000/ 	| Minio service endpoint url to enable secor use MinIO as deepstorage. 	|
|  	| aws_region 	| "us-east-2" 	| Deepstorage container region. 	|
|  	| secor_s3_bucket 	| "secor-bucket" 	| Deepstorage container name. 	|
| AZURE 	| upload_manager 	| "com.pinterest.secor.uploader.AzureUploadManager" 	| Blob upload manager which is responsible to upload backup to deepstorage. 	|
|  	| cloud_store_provider 	| "blob" 	| Type of the deepstorage. 	|
|  	| azure_account_name 	| "" 	| Account key to access the blob storage. 	|
|  	| azure_account_key 	| "" 	| Account secret to access the blob storage. 	|
|  	| azure_container_name 	| "secor-bucket" 	| Deepstorage container name. 	|
| GCP 	| upload_manger 	| "com.pinterest.secor.uploader.GsUploadManager" 	| Google cloud upload manager which is responsible to upload backup to deepstorage. 	|
|  	| gs_bucket 	| "secor-bucket" 	| Deepstorage container name. 	|
|  	| gs_path 	| "/telemetry-data/" 	| Path inside deepstorage where the secor backups are stored. 	|
|  	| gs_credentials_path 	| "google_app_credentials.json" 	| Credentials path where access token and secrets are stored. 	|