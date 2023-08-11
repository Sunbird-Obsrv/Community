**Druid:**
| AWS 	| MinIO 	| AZURE 	| GCP 	|
|---	|---	|---	|---	|
| `druid_deepstorage_type: "s3"` <br>`s3_access_key: ""`<br>`s3_secret_key: ""`<br>`s3_bucket: "”`<br>`druid_indexer_logs_prefix:""`<br>`druid_storage_baseKey:""` 	| `druid_s3_endpoint_url:""`<br>`druid_storage_baseKey:""`<br>`s3_access_key: ""`<br>`s3_secret_key: ""`<br>`s3_bucket: "”`<br>`druid_s3_endpoint_signingRegion:””`<br>`druid_indexer_logs_directory:””` 	| `azure_storage_account_name:""`<br>`azure_storage_account_key:””`<br>`azure_storage_container:””` 	| `gcs_bucket:""`<br>`google_application_credentials:""`<br>`druid_storage_baseKey:""` 	|

**Flink:**
| AWS 	| MinIO 	| AZURE 	| GCP 	|
|---	|---	|---	|---	|
| `s3_access_key:""` `s3_secret_key:""` `s3_endpoint:""` `base.url="s3://"` 	| `s3_access_key:""` `s3_secret_key:""` `s3_endpoint:""` `base.url="s3://"` 	| `azure_account:""` `azure_secret:""` `base.url="blob://"` 	| `google_service_account_key_path:""` 	|

**Secor:**

| AWS 	| MinIO 	| AZURE 	| GCP 	|
|---	|---	|---	|---	|
| `upload_manager:"com.pinterest.secor.uploader.S3UploadManager"`<br>`cloud_store_provider:"s3"`<br>`aws_access_key=""`<br>`aws_secret_key=""`<br>`aws_region=""`<br>`aws_endpoint=""`<br>`secor_s3_bucket=""` 	| `upload_manager:"com.pinterest.secor.uploader.S3UploadManager"`<br>`cloud_store_provider:"s3"`<br>`aws_access_key:""`<br>`aws_secret_key:""`<br>`aws_region:""`<br>`aws_endpoint:""`<br>`secor_s3_bucket:""` 	| `upload_manager:"com.pinterest.secor.uploader.AzureUploadManager"`<br>`cloud_store_provider:"blob"`<br>`azure_account_name:""`<br>`azure_account_key=`<br>`azure_container_name=` 	| `upload_manger:"com.pinterest.secor.uploader.GsUploadManager"`<br>`gs_bucket:""`<br>`gs_path:""`<br>`gs_credentials_path:""` 	|