**Druid:**                                      
<table>
<thead>
  <tr>
    <th></th>
    <th>Key</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="5">AWS</td>
    <td>druid_deepstorage_type</td>
    <td>S3</td>
    <td>Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>druid_indexer_logs_prefix</td>
    <td>"backups/druid/druid-task-logs"</td>
    <td>Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td>"druid/segments"</td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td rowspan="8">MinIO</td>
    <td>druid_deepstorage_type</td>
    <td>S3</td>
    <td>Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td>druid_s3_endpoint_url</td>
    <td>http://172.20.126.232:9000/</td>
    <td>Minio service endpoint url to enable druid use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td>"druid/segments"</td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_bucket</td>
    <td>"druid-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>druid_s3_endpoint_signingRegion</td>
    <td>"us-east-2"</td>
    <td>Region where the deepstorage container created.</td>
  </tr>
  <tr>
    <td>druid_indexer_logs_directory</td>
    <td>"backups/druid/druid-task-logs"</td>
    <td>Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td rowspan="3">AZURE</td>
    <td>azure_storage_account_name</td>
    <td>"druid-blob"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>azure_storage_account_key</td>
    <td>"druid/segments"</td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td>druid_storage_directory</td>
    <td>"/data"</td>
    <td>Root path inside the blob storage where all the druid data is pushed.</td>
  </tr>
  <tr>
    <td rowspan="3">GCP</td>
    <td>gcs_bucket</td>
    <td>"druid-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>google_application_credentials</td>
    <td>""</td>
    <td>Google cloud credentials json file where the access_token and credentials are stored.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td>"druid/segments"</td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
</tbody>
</table>

**Flink:**
<table>
<thead>
  <tr>
    <th></th>
    <th>Key</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="4">AWS</td>
    <td>checkpoint_store_type</td>
    <td>S3</td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td>"s3://flink-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td rowspan="5">MinIO</td>
    <td>checkpoint_store_type</td>
    <td>S3</td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_endpoint</td>
    <td>"http://172.20.126.232:9000"</td>
    <td>Minio service endpoint url  to enable flink use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td>"s3://flink-bucket"</td>
    <td>Deepstorage container url.</td>
  </tr>
  <tr>
    <td rowspan="4">AZURE</td>
    <td>checkpoint_store_type</td>
    <td>"Blob"</td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>azure_account</td>
    <td>""</td>
    <td>Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_secret</td>
    <td>""</td>
    <td>Secret key to access the blob.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td>"blob://flink-bucket"</td>
    <td>Deepstorage container url.</td>
  </tr>
  <tr>
    <td rowspan="2">GCP</td>
    <td>checkpoint_store_type</td>
    <td>"gcp"</td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>google_service_account_key_path</td>
    <td>"/data/flink/gcp_cred.conf"</td>
    <td>Configmap path where google credentials are stored and mounted.The credential path needs to exposed as environment variable.</td>
  </tr>
</tbody>
</table>

**Secor:**

<table>
<thead>
  <tr>
    <th></th>
    <th>Key</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="7">AWS</td>
    <td>upload_manager</td>
    <td><code>com.pinterest.secor.uploader.S3UploadManager</code></td>
    <td>s3 upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td>cloud_store_provider</td>
    <td>"S3"</td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>aws_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_endpoint</td>
    <td>https://secor-bucket.s3.us-east-2.amazonaws.com/</td>
    <td>Bucket endpoint url where all the secor backups are pushed.</td>
  </tr>
  <tr>
    <td>secor_s3_bucket</td>
    <td>"secor-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>aws_region</td>
    <td>"us-east-2"</td>
    <td>Deepstorage container region.</td>
  </tr>
  <tr>
    <td rowspan="7">MinIO</td>
    <td>upload_manager</td>
    <td><code>com.pinterest.secor.uploader.S3UploadManager</code></td>
    <td>s3 upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td>cloud_store_provider</td>
    <td>"S3"</td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>aws_access_key</td>
    <td>""</td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_secret_key</td>
    <td>""</td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_endpoint</td>
    <td>http://172.20.126.232:9000/</td>
    <td>Minio service endpoint url to enable secor use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>aws_region</td>
    <td>"us-east-2"</td>
    <td>Deepstorage container region.</td>
  </tr>
  <tr>
    <td>secor_s3_bucket</td>
    <td>"secor-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td rowspan="5">AZURE</td>
    <td>upload_manager</td>
    <td><code>com.pinterest.secor.uploader.AzureUploadManager</code></td>
    <td>Blob upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td>cloud_store_provider</td>
    <td>"blob"</td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>azure_account_name</td>
    <td>""</td>
    <td>Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_account_key</td>
    <td>""</td>
    <td>Account secret to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_container_name</td>
    <td>"secor-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td rowspan="4">GCP</td>
    <td>upload_manger</td>
    <td><code>com.pinterest.secor.uploader.GsUploadManager</code></td>
    <td>Google cloud upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td>gs_bucket</td>
    <td>"secor-bucket"</td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>gs_path</td>
    <td>"/telemetry-data/"</td>
    <td>Path inside deepstorage where the secor backups are stored.</td>
  </tr>
  <tr>
    <td>gs_credentials_path</td>
    <td>"google_app_credentials.json"</td>
    <td>Credentials path where access token and secrets are stored.</td>
  </tr>
</tbody>
</table>
