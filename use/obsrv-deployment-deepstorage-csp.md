**Druid:**                                      
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-cly1{text-align:left;vertical-align:middle}
.tg .tg-0lax{text-align:left;vertical-align:top}
.tg .tg-nrix{text-align:center;vertical-align:middle}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0lax"></th>
    <th class="tg-0lax">Key</th>
    <th class="tg-0lax">Value</th>
    <th class="tg-0lax">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-nrix" rowspan="5">AWS</td>
    <td class="tg-0lax">druid_deepstorage_type</td>
    <td class="tg-0lax">S3</td>
    <td class="tg-0lax">Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_indexer_logs_prefix</td>
    <td class="tg-0lax">"backups/druid/druid-task-logs"</td>
    <td class="tg-0lax">Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_storage_baseKey</td>
    <td class="tg-0lax">"druid/segments"</td>
    <td class="tg-0lax">Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="8">MinIO</td>
    <td class="tg-0lax">druid_deepstorage_type</td>
    <td class="tg-0lax">S3</td>
    <td class="tg-0lax">Deepstorage type where the needs to be pushed.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_s3_endpoint_url</td>
    <td class="tg-0lax">http://172.20.126.232:9000/</td>
    <td class="tg-0lax">Minio service endpoint url to enable druid use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_storage_baseKey</td>
    <td class="tg-0lax">"druid/segments"</td>
    <td class="tg-0lax">Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_bucket</td>
    <td class="tg-0lax">"druid-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_s3_endpoint_signingRegion</td>
    <td class="tg-0lax">"us-east-2"</td>
    <td class="tg-0lax">Region where the deepstorage container created.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_indexer_logs_directory</td>
    <td class="tg-0lax">"backups/druid/druid-task-logs"</td>
    <td class="tg-0lax">Path inside the bucket where we wanted to store indexer logs.</td>
  </tr>
  <tr>
    <td class="tg-cly1" rowspan="3">AZURE</td>
    <td class="tg-0lax">azure_storage_account_name</td>
    <td class="tg-0lax">"druid-blob"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_storage_account_key</td>
    <td class="tg-0lax">"druid/segments"</td>
    <td class="tg-0lax">Path inside the bucket where all the segments are stored.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_storage_directory</td>
    <td class="tg-0lax">"/data"</td>
    <td class="tg-0lax">Root path inside the blob storage where all the druid data is pushed.</td>
  </tr>
  <tr>
    <td class="tg-cly1" rowspan="3">GCP</td>
    <td class="tg-0lax">gcs_bucket</td>
    <td class="tg-0lax">"druid-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-0lax">google_application_credentials</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Google cloud credentials json file where the access_token and credentials are stored.</td>
  </tr>
  <tr>
    <td class="tg-0lax">druid_storage_baseKey</td>
    <td class="tg-0lax">"druid/segments"</td>
    <td class="tg-0lax">Path inside the bucket where all the segments are stored.</td>
  </tr>
</tbody>
</table>

**Flink:**
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-0lax{text-align:left;vertical-align:top}
.tg .tg-nrix{text-align:center;vertical-align:middle}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0lax"></th>
    <th class="tg-0lax">Key</th>
    <th class="tg-0lax">Value</th>
    <th class="tg-0lax">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-nrix" rowspan="4">AWS</td>
    <td class="tg-0lax">checkpoint_store_type</td>
    <td class="tg-0lax">S3</td>
    <td class="tg-0lax">Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">base.url</td>
    <td class="tg-0lax">"s3://flink-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="5">MinIO</td>
    <td class="tg-0lax">checkpoint_store_type</td>
    <td class="tg-0lax">S3</td>
    <td class="tg-0lax">Type of the deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">s3_endpoint</td>
    <td class="tg-0lax">"http://172.20.126.232:9000"</td>
    <td class="tg-0lax">Minio service endpoint url&nbsp;&nbsp;to enable flink use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">base.url</td>
    <td class="tg-0lax">"s3://flink-bucket"</td>
    <td class="tg-0lax">Deepstorage container url.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="4">AZURE</td>
    <td class="tg-0lax">checkpoint_store_type</td>
    <td class="tg-0lax">"Blob"</td>
    <td class="tg-0lax">Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_account</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_secret</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the blob.</td>
  </tr>
  <tr>
    <td class="tg-0lax">base.url</td>
    <td class="tg-0lax">"blob://flink-bucket"</td>
    <td class="tg-0lax">Deepstorage container url.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="2">GCP</td>
    <td class="tg-0lax">checkpoint_store_type</td>
    <td class="tg-0lax">"gcp"</td>
    <td class="tg-0lax">Type of the deepstorage container.</td>
  </tr>
  <tr>
    <td class="tg-0lax">google_service_account_key_path</td>
    <td class="tg-0lax">"/data/flink/gcp_cred.conf"</td>
    <td class="tg-0lax">Configmap path where google credentials are stored and mounted.The credential path needs to exposed as environment variable.</td>
  </tr>
</tbody>
</table>

**Secor:**

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-0lax{text-align:left;vertical-align:top}
.tg .tg-nrix{text-align:center;vertical-align:middle}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-0lax"></th>
    <th class="tg-0lax">Key</th>
    <th class="tg-0lax">Value</th>
    <th class="tg-0lax">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-nrix" rowspan="7">AWS</td>
    <td class="tg-0lax">upload_manager</td>
    <td class="tg-0lax">"com.pinterest.secor.uploader.S3UploadManager"</td>
    <td class="tg-0lax">s3 upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">cloud_store_provider</td>
    <td class="tg-0lax">"S3"</td>
    <td class="tg-0lax">Type of the deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_endpoint</td>
    <td class="tg-0lax">https://secor-bucket.s3.us-east-2.amazonaws.com/</td>
    <td class="tg-0lax">Bucket endpoint url where all the secor backups are pushed.</td>
  </tr>
  <tr>
    <td class="tg-0lax">secor_s3_bucket</td>
    <td class="tg-0lax">"secor-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_region</td>
    <td class="tg-0lax">"us-east-2"</td>
    <td class="tg-0lax">Deepstorage container region.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="7">MinIO</td>
    <td class="tg-0lax">upload_manager</td>
    <td class="tg-0lax">"com.pinterest.secor.uploader.S3UploadManager"</td>
    <td class="tg-0lax">s3 upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">cloud_store_provider</td>
    <td class="tg-0lax">"S3"</td>
    <td class="tg-0lax">Type of the deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_access_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Access key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_secret_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Secret key to access the bucket.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_endpoint</td>
    <td class="tg-0lax">http://172.20.126.232:9000/</td>
    <td class="tg-0lax">Minio service endpoint url to enable secor use MinIO as deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">aws_region</td>
    <td class="tg-0lax">"us-east-2"</td>
    <td class="tg-0lax">Deepstorage container region.</td>
  </tr>
  <tr>
    <td class="tg-0lax">secor_s3_bucket</td>
    <td class="tg-0lax">"secor-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="5">AZURE</td>
    <td class="tg-0lax">upload_manager</td>
    <td class="tg-0lax">"com.pinterest.secor.uploader.AzureUploadManager"</td>
    <td class="tg-0lax">Blob upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">cloud_store_provider</td>
    <td class="tg-0lax">"blob"</td>
    <td class="tg-0lax">Type of the deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_account_name</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Account key to access the blob storage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_account_key</td>
    <td class="tg-0lax">""</td>
    <td class="tg-0lax">Account secret to access the blob storage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">azure_container_name</td>
    <td class="tg-0lax">"secor-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-nrix" rowspan="4">GCP</td>
    <td class="tg-0lax">upload_manger</td>
    <td class="tg-0lax">"com.pinterest.secor.uploader.GsUploadManager"</td>
    <td class="tg-0lax">Google cloud upload manager which is responsible to upload backup to deepstorage.</td>
  </tr>
  <tr>
    <td class="tg-0lax">gs_bucket</td>
    <td class="tg-0lax">"secor-bucket"</td>
    <td class="tg-0lax">Deepstorage container name.</td>
  </tr>
  <tr>
    <td class="tg-0lax">gs_path</td>
    <td class="tg-0lax">"/telemetry-data/"</td>
    <td class="tg-0lax">Path inside deepstorage where the secor backups are stored.</td>
  </tr>
  <tr>
    <td class="tg-0lax">gs_credentials_path</td>
    <td class="tg-0lax">"google_app_credentials.json"</td>
    <td class="tg-0lax">Credentials path where access token and secrets are stored.</td>
  </tr>
</tbody>
</table>