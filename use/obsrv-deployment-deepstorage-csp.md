**Druid:**
|  	| Key 	| Value 	| Description 	|
|---	|---	|---	|---	|
| AWS 	| druid_deepstorage_type 	| S3 	| Deepstorage type where the needs to be pushed. 	|
|  	| s3_access_key 	| "" 	| Access key to access the bucket. 	|
|  	| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
|  	| druid_indexer_logs_prefix 	| "backups/druid/druid-task-logs" 	| Path inside the bucket where we wanted to store indexer logs. 	|
|  	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored.  	|
| MinIO 	| druid_deepstorage_type 	| S3 	| Deepstorage type where the needs to be pushed. 	|
|  	| druid_s3_endpoint_url 	| http://172.20.126.232:9000/ 	| Minio service ip to be provided to make druid use MinIO as deepstorage. 	|
|  	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|
|  	| s3_access_key 	| "" 	| Access key to access the bucket. 	|
|  	| s3_secret_key 	| "" 	| Secret key to access the bucket. 	|
|  	| s3_bucket 	| "druid-bucket" 	| Deepstorage container name. 	|
|  	| druid_s3_endpoint_signingRegion 	| "us-east-2" 	| Region where the deepstorage container created. 	|
|  	| druid_indexer_logs_directory 	| "backups/druid/druid-task-logs" 	| Path inside the bucket where we wanted to store indexer logs. 	|
| AZURE 	| azure_storage_account_name 	| "druid-blob" 	| Deepstorage container name. 	|
|  	| azure_storage_account_key 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|
|  	| druid_storage_directory 	| "/data" 	| Root path inside the blob storage where all the druid data is pushed. 	|
| GCP 	| gcs_bucket 	| "druid-bucket" 	| Deepstorage container name. 	|
|  	| google_application_credentials 	| "" 	| Google cloud credentials json file where the access_token and credentials are stored. 	|
|  	| druid_storage_baseKey 	| "druid/segments" 	| Path inside the bucket where all the segments are stored. 	|

**Flink:**
| AWS 	| MinIO 	| AZURE 	| GCP 	|
|---	|---	|---	|---	|
| `checkpoint_store_type:""`<br>`s3_access_key:""`<br> `s3_secret_key:""`<br> `s3_endpoint:""`<br> `base.url="s3://"`<br> 	| `checkpoint_store_type:""`<br>`s3_access_key:""`<br> `s3_secret_key:""`<br> `s3_endpoint:""`<br> `base.url="s3://"`<br> 	| `checkpoint_store_type:""`<br>`azure_account:""`<br> `azure_secret:""`<br> `base.url="blob://"`<br> 	| `checkpoint_store_type:""`<br>`google_service_account_key_path:""` 	|

**Secor:**

| AWS 	| MinIO 	| AZURE 	| GCP 	|
|---	|---	|---	|---	|
| `upload_manager:"com.pinterest.secor.uploader.S3UploadManager"`<br>`cloud_store_provider:"s3"`<br>`aws_access_key=""`<br>`aws_secret_key=""`<br>`aws_region=""`<br>`aws_endpoint=""`<br>`secor_s3_bucket=""` 	| `upload_manager:"com.pinterest.secor.uploader.S3UploadManager"`<br>`cloud_store_provider:"s3"`<br>`aws_access_key:""`<br>`aws_secret_key:""`<br>`aws_region:""`<br>`aws_endpoint:""`<br>`secor_s3_bucket:""` 	| `upload_manager:"com.pinterest.secor.uploader.AzureUploadManager"`<br>`cloud_store_provider:"blob"`<br>`azure_account_name:""`<br>`azure_account_key=`<br>`azure_container_name=` 	| `upload_manger:"com.pinterest.secor.uploader.GsUploadManager"`<br>`gs_bucket:""`<br>`gs_path:""`<br>`gs_credentials_path:""` 	|