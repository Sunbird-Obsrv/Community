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
    <td><code>"S3"</code></td>
    <td>Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td><code>""</code></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>druid_indexer_logs_prefix</td>
    <td><code>"backups/druid/druid-task-logs"</code></td>
    <td>Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td><code>"druid/segments"</code></td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td rowspan="8">MinIO</td>
    <td>druid_deepstorage_type</td>
    <td><code>S3</code></td>
    <td>Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td>druid_s3_endpoint_url</td>
    <td><code>http://172.20.126.232:9000/</code></td>
    <td>Minio service endpoint url to enable druid use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td><code>"druid/segments"</code></td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td><code>""</code></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_bucket</td>
    <td><code>"druid-bucket"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>druid_s3_endpoint_signingRegion</td>
    <td><code>"us-east-2"</code></td>
    <td>Region where the deepstorage container created.</td>
  </tr>
  <tr>
    <td>druid_indexer_logs_directory</td>
    <td><code>"backups/druid/druid-task-logs"</code></td>
    <td>Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td rowspan="3">AZURE</td>
    <td>azure_storage_account_name</td>
    <td><code>"druid-blob"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>azure_storage_account_key</td>
    <td><code>"druid/segments"</code></td>
    <td>Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td>druid_storage_directory</td>
    <td><code>"/data"</code></td>
    <td>Root path inside the blob storage where all the druid data is pushed.</td>
  </tr>
  <tr>
    <td rowspan="3">GCP</td>
    <td>gcs_bucket</td>
    <td><code>"druid-bucket"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>google_application_credentials</td>
    <td><code>""</code></td>
    <td>Google cloud credentials json file where the access_token and credentials are stored.</td>
  </tr>
  <tr>
    <td>druid_storage_baseKey</td>
    <td><code>"druid/segments"</code></td>
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
    <td><code>"S3"</code></td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td><code>""</code></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td><code>"s3://flink-bucket"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td rowspan="5">MinIO</td>
    <td>checkpoint_store_type</td>
    <td><code>"S3"</code"></td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>s3_access_key</td>
    <td><code>""</code></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>s3_endpoint</td>
    <td><code>"http://172.20.126.232:9000"</code></td>
    <td>Minio service endpoint url  to enable flink use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td><code>"s3://flink-bucket"</code></td>
    <td>Deepstorage container url.</td>
  </tr>
  <tr>
    <td rowspan="4">AZURE</td>
    <td>checkpoint_store_type</td>
    <td><code>"Blob"</code></td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>azure_account</td>
    <td><code>""</code></td>
    <td>Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_secret</td>
    <td><code>""</code></td>
    <td>Secret key to access the blob.</td>
  </tr>
  <tr>
    <td>base.url</td>
    <td><code>"blob://flink-bucket"</code></td>
    <td>Deepstorage container url.</td>
  </tr>
  <tr>
    <td rowspan="2">GCP</td>
    <td>checkpoint_store_type</td>
    <td><code>"gcp"</code></td>
    <td>Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td>google_service_account_key_path</td>
    <td><code>"/data/flink/gcp_cred.conf"</code></td>
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
    <td><code>"S3"</code></td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>aws_access_key</td>
    <td><code>""</code></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_endpoint</td>
    <td><code>"https://secor-bucket.s3.us-east-2.amazonaws.com/"</code></td>
    <td>Bucket endpoint url where all the secor backups are pushed.</td>
  </tr>
  <tr>
    <td>secor_s3_bucket</td>
    <td><code>"secor-bucket"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>aws_region</td>
    <td><code>"us-east-2"</code></td>
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
    <td><code>"S3"</code></td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>aws_access_key</td>
    <td><code>""</cdoe></td>
    <td>Access key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_secret_key</td>
    <td><code>""</code></td>
    <td>Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td>aws_endpoint</td>
    <td><code>"http://172.20.126.232:9000/"</code></td>
    <td>Minio service endpoint url to enable secor use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td>aws_region</td>
    <td><code>"us-east-2"</code></td>
    <td>Deepstorage container region.</td>
  </tr>
  <tr>
    <td>secor_s3_bucket</td>
    <td><code>"secor-bucket"</code></td>
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
    <td><code>"blob"</code></td>
    <td>Type of the deepstorage.</td>
  </tr>
  <tr>
    <td>azure_account_name</td>
    <td><code>""</code></td>
    <td>Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_account_key</td>
    <td><code>""</code></td>
    <td>Account secret to access the blob storage.</td>
  </tr>
  <tr>
    <td>azure_container_name</td>
    <td><code>"secor-bucket"</code></td>
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
    <td><code>"secor-bucket"</code></td>
    <td>Deepstorage container name.</td>
  </tr>
  <tr>
    <td>gs_path</td>
    <td><code>"/telemetry-data/"</code></td>
    <td>Path inside deepstorage where the secor backups are stored.</td>
  </tr>
  <tr>
    <td>gs_credentials_path</td>
    <td><code>"google_app_credentials.json"</code></td>
    <td>Credentials path where access token and secrets are stored.</td>
  </tr>
</tbody>
</table>
