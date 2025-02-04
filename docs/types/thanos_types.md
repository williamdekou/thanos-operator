### ThanosSpec
#### ThanosSpec defines the desired state of Thanos

| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| queryDiscovery | bool | No | - |  |
| storeGateway | *StoreGateway | No | - |  |
| rule | *Rule | No | - |  |
| query | *Query | No | - |  |
| queryFrontend | *QueryFrontend | No | - |  |
| clusterDomain | string | No | - |  |
| enableRecreateWorkloadOnImmutableFieldChange | bool | No | - |  |
### Metrics
#### Metrics defines the service monitor endpoints

| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| interval | string | No | - |  |
| timeout | string | No | - |  |
| port | int32 | No | - |  |
| path | string | No | - |  |
| serviceMonitor | bool | No | - |  |
| prometheusAnnotations | bool | No | - |  |
### Ingress
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| ingressOverrides | *typeoverride.IngressNetworkingV1beta1 | No | - |  |
| certificate | string | No | - | Certificate in the ingress namespace<br> |
| host | string | No | - |  |
| path | string | No | - |  |
### QueryFrontend
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| metaOverrides | *typeoverride.ObjectMeta | No | - |  |
| deploymentOverrides | *typeoverride.Deployment | No | - |  |
| serviceOverrides | *typeoverride.Service | No | - |  |
| metrics | *Metrics | No | - |  |
| HTTPIngress | *Ingress | No | - |  |
| logLevel | string | No | - |  |
| logFormat | string | No | - |  |
| queryRangeSplit | string | No | - | Split queries by an interval and execute in parallel, 0 disables it.<br> |
| queryRangeMaxRetriesPerRequest | int | No | - | Maximum number of retries for a single request; beyond this, the downstream error is returned.<br> |
| queryRangeMaxQueryLength | int | No | - | Limit the query time range (end - start time) in the query-frontend, 0 disables it.<br> |
| queryRangeMaxQueryParallelism | int | No | - | Maximum number of queries will be scheduled in parallel by the frontend.<br> |
| queryRangeResponseCacheMaxFreshness | string | No | - | Most recent allowed cacheable result, to prevent	caching very recent results that might still be in flux.<br> |
| queryRangePartialResponse | *bool | No | - | Enable partial response for queries if no partial_response param is specified.<br> |
| queryRangeResponseCacheConfigFile | string | No | - | Path to YAML file that contains response cache configuration.<br> |
| queryRangeResponseCache | string | No | - | Alternative to 'query-range.response-cache-config-file' flag (lower priority). Content of YAML file that contains response cache configuration.<br> |
| httpAddress | string | No | - | Listen host:port for HTTP endpoints.<br> |
| http_grace_period | string | No | - | Time to wait after an interrupt received for HTTP Server.<br> |
| queryFrontendDownstreamURL | string | No | - | URL of downstream Prometheus Query compatible API.<br> |
| queryFrontendCompressResponses | *bool | No | - | Compress HTTP responses.<br> |
| queryFrontendLogQueriesLongerThan | int | No | - | Log queries that are slower than the specified duration. Set to 0 to disable. Set to < 0 to enable on all queries.<br> |
| logRequestDecision | string | No | - | Request Logging for logging the start and end of requests. LogFinishCall is enabled by default.<br>LogFinishCall : Logs the finish call of the requests.<br>LogStartAndFinishCall : Logs the start and finish call of the requests.<br>NoLogCall : Disable request logging.<br> |
### Query
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| metaOverrides | typeoverride.ObjectMeta | No | - |  |
| deploymentOverrides | *typeoverride.Deployment | No | - |  |
| serviceOverrides | *typeoverride.Service | No | - |  |
| metrics | *Metrics | No | - |  |
| HTTPIngress | *Ingress | No | - |  |
| GRPCIngress | *Ingress | No | - |  |
| GRPCClientCertificate | string | No | - | Cert and key expected under tls.crt, tls.key<br> |
| GRPCClientCA | string | No | - | CA bundle to verify servers against, expected under ca.crt<br> |
| GRPCClientServerName | string | No | - | Server name to verify server certificate against<br> |
| GRPCServerCertificate | string | No | - | Cert and key expected under tls.crt, tls.key<br> |
| GRPCServerCA | string | No | - | CA bundle to verify clients against, expected under ca.crt<br> |
| logLevel | string | No | - |  |
| logFormat | string | No | - |  |
| httpAddress | string | No | - | Listen host:port for HTTP endpoints.<br> |
| http_grace_period | string | No | - | Time to wait after an interrupt received for HTTP Server.<br> |
| grpcAddress | string | No | - | Listen ip:port address for gRPC endpoints<br> |
| grpcGracePeriod | string | No | - | Time to wait after an interrupt received for GRPC Server.<br> |
| webRoutePrefix | string | No | - | Prefix for API and UI endpoints. This allows thanos UI to be served on a sub-path. This<br>option is analogous to --web.route-prefix of Promethus.<br> |
| webExternalPrefix | string | No | - | Static prefix for all HTML links and redirect URLs in the UI query web interface. Actual<br>endpoints are still served on / or the web.route-prefix. This allows thanos UI to be<br>served behind a reverse proxy that strips a URL sub-path.<br> |
| webPrefixHeader | string | No | - | Name of HTTP request header used for dynamic prefixing of UI links and redirects. This<br>option is ignored if web.external-prefix argument is set. Security risk: enable this<br>option only if a reverse proxy in front of thanos is resetting the header. The<br>--web.prefix-header=X-Forwarded-Prefix option can be useful, for example, if Thanos UI is<br>served via Traefik reverse proxy with PathPrefixStrip option enabled, which sends the<br>stripped prefix value in X-Forwarded-Prefix header. This allows thanos UI to be served on a<br>sub-path.<br> |
| queryTimeout | metav1.Duration | No | - | Maximum time to process query by query node.<br> |
| queryMaxConcurrent | int | No | - | Maximum number of queries processed concurrently by query node.<br> |
| queryReplicaLabel | []string | No | - | Labels to treat as a replica indicator along which data is deduplicated. Still you will be<br>able to query without deduplication using 'dedup=false' parameter.<br> |
| selectorLabels | map[string]string | No | - | Query selector labels that will be exposed in info endpoint (repeated).<br> |
| stores | []string | No | - | Addresses of statically configured store API servers (repeatable). The scheme may be<br>prefixed with 'dns+' or 'dnssrv+' to detect store API servers through respective DNS lookups.<br> |
| storeSDDNSInterval | metav1.Duration | No | - | Interval between DNS resolutions.<br> |
| storeUnhealthyTimeout | metav1.Duration | No | - | Timeout before an unhealthy store is cleaned from the store UI page.<br> |
| queryAutoDownsampling | bool | No | - | Enable automatic adjustment (step / 5) to what source of data should be used in store gateways<br>if no max_source_resolution param is specified.<br> |
| queryPartialResponse | bool | No | - | Enable partial response for queries if no partial_response param is specified.<br> |
| queryDefaultEvaluationInterval | metav1.Duration | No | - | Set default evaluation interval for sub queries.<br> |
| storeResponseTimeout | metav1.Duration | No | - | If a Store doesn't send any data in this specified duration then a Store will be ignored<br>and partial data will be returned if it's enabled. 0 disables timeout.<br> |
### ThanosDiscovery
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
|  | metav1.LabelSelector | No | - |  |
### TimeRange
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| minTime | string | No | - | Start of time range limit to serve. Thanos Store will serve only metrics, which happened<br>later than this value. Option can be a constant time in RFC3339 format or time duration<br>relative to current time, such as -1d or 2h45m. Valid duration units are ms, s, m, h, d, w, y.<br> |
| maxTime | string | No | - | End of time range limit to serve. Thanos Store<br>will serve only blocks, which happened eariler<br>than this value. Option can be a constant time<br>in RFC3339 format or time duration relative to<br>current time, such as -1d or 2h45m. Valid<br>duration units are ms, s, m, h, d, w, y.<br> |
### StoreGateway
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| metaOverrides | *typeoverride.ObjectMeta | No | - |  |
| deploymentOverrides | *typeoverride.Deployment | No | - |  |
| serviceOverride | *typeoverride.Service | No | - |  |
| metrics | *Metrics | No | - |  |
| GRPCServerCertificate | string | No | - |  |
| logLevel | string | No | - |  |
| logFormat | string | No | - |  |
| httpAddress | string | No | - | Listen host:port for HTTP endpoints.<br> |
| http_grace_period | string | No | - | Time to wait after an interrupt received for HTTP Server.<br> |
| grpcAddress | string | No | - | Listen ip:port address for gRPC endpoints<br> |
| grpcGracePeriod | string | No | - | Time to wait after an interrupt received for GRPC Server.<br> |
| indexCacheSize | string | No | - | Maximum size of items held in the in-memory index cache.<br> |
| indexCacheConfigFile | string | No | - | Path to YAML file that contains index cache configuration. See format details:<br>https://thanos.io/tip/components/store.md/#index-cache<br> |
| indexCacheConfig | string | No | - | Alternative to 'index-cache.config-file' flag (lower priority). Content of YAML file that contains index cache configuration. See format details:<br>https://thanos.io/tip/components/store.md/#index-cache<br> |
| chunkPoolSize | string | No | - | Maximum size of concurrently allocatable bytes for chunks.<br> |
| storeGRPCSeriesSampleLimit | string | No | - | Maximum amount of samples returned via a single Series call. 0 means no limit. NOTE: For<br>efficiency we take 120 as the number of samples in chunk (it cannot be bigger than that), so<br>the actual number of samples might be lower, even though the maximum could be hit.<br> |
| storeGRPCTouchedSeriesSampleLimit | int | No | - | Maximum amount of touched series returned via a single Series call. The Series call fails if this limit is exceeded. 0 means no limit.<br> |
| storeGRPCSeriesMaxConcurrency | int | No | - | Maximum number of concurrent Series calls.<br> |
| syncBlockDuration | string | No | - | Repeat interval for syncing the blocks between local and remote view.<br> |
| blockSyncConcurrency | int | No | - | Number of goroutines to use when constructing index-cache.json blocks from object storage.<br> |
| blockMetaFetchConcurrency | int | No | - | Number of goroutines to use when fetching block metadata from object storage.<br> |
| selectorRelabelConfigFile | string | No | - | Path to YAML file that contains relabeling configuration that allows selecting blocks. It<br>follows native Prometheus relabel-config syntax. See format details:<br>https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config<br> |
| selectorRelabelConfig | string | No | - | Alternative to 'selector.relabel-config-file' flag (lower priority). Content of YAML file<br>that contains relabeling configuration that allows selecting blocks. It follows native<br>Prometheus relabel-config syntax. See format details:<br>https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config<br> |
| consistencyDelay | string | No | - | Minimum age of all blocks before they are being read. Set it to safe value (e.g 30m) if your<br>object storage is eventually consistent. GCS and S3 are (roughly) strongly consistent.<br> |
| ignoreDeletionMarksDelay | string | No | - | Duration after which the blocks marked for deletion will be filtered out while fetching blocks. The idea of ignore-deletion-marks-delay<br>is to ignore blocks that are marked for deletion with some delay. This ensures store can still serve blocks that are meant to be<br>deleted but do not have a replacement yet. If delete-delay duration is provided to compactor or bucket verify component, it will upload<br>deletion-mark.json file to mark after what duration the block should be deleted rather than deleting the block straight away. If<br>delete-delay is non-zero for compactor or bucket verify component, ignore-deletion-marks-delay should be set to<br>(delete-delay)/2 so that blocks marked for deletion are filtered out while fetching blocks<br>before being deleted from bucket. Default is 24h, half of the default value for --delete-delay on compactor.<br> |
| storeEnableIndexHeaderLazyReader | *bool | No | - | If true, Store Gateway will lazy memory map index-header only once the block is required by a query.<br> |
| webExternalPrefix | string | No | - | Static prefix for all HTML links and redirect URLs in the bucket web UI interface. Actual endpoints are still served on / or the<br>web.route-prefix. This allows thanos bucket web UI to be served behind a reverse proxy that<br>strips a URL sub-path.<br> |
| webPrefixHeader | string | No | - | Name of HTTP request header used for dynamic prefixing of UI links and redirects. This<br>option is ignored if web.external-prefix argument is set. Security risk: enable this<br>option only if a reverse proxy in front of thanos is resetting the header. The<br>--web.prefix-header=X-Forwarded-Prefix option can be useful, for example, if Thanos UI is<br>served via Traefik reverse proxy with PathPrefixStrip option enabled, which sends the<br>stripped prefix value in X-Forwarded-Prefix header. This allows thanos UI to be served on a sub-path.<br> |
| timeRanges | []TimeRange | No | - | TimeRanges is a list of TimeRange to partition Store Gateway<br> |
### Rule
| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
| metaOverrides | *typeoverride.ObjectMeta | No | - |  |
| statefulsetOverrides | *typeoverride.StatefulSet | No | - |  |
| serviceOverrides | *typeoverride.Service | No | - |  |
| metrics | *Metrics | No | - |  |
| HTTPIngress | *Ingress | No | - |  |
| GRPCIngress | *Ingress | No | - |  |
| logLevel | string | No | - |  |
| logFormat | string | No | - |  |
| httpAddress | string | No | - | Listen host:port for HTTP endpoints.<br> |
| http_grace_period | string | No | - | Time to wait after an interrupt received for HTTP Server.<br> |
| dataDir | string | No | - | Data directory.<br> |
| dataVolume | *volume.KubernetesVolume | No | - | Kubernetes volume abstraction refers to different types of volumes to be mounted to pods: emptyDir, hostPath, pvc.<br> |
| grpcAddress | string | No | - | Listen ip:port address for gRPC endpoints<br> |
| grpcGracePeriod | string | No | - | Time to wait after an interrupt received for GRPC Server.<br> |
| labels | map[string]string | No | - | Labels to be applied to all generated metrics<br>(repeated). Similar to external labels for<br>Prometheus, used to identify ruler and its<br>blocks as unique source.<br> |
| rules | string | No | - | Rules<br> |
| resendDelay | string | No | - | Minimum amount of time to wait before resending an alert to Alertmanager.<br> |
| evalInterval | string | No | - | The default evaluation interval to use.<br> |
| tsdbBlockDuration | string | No | - | Block duration for TSDB block.<br> |
| tsdbRetention | string | No | - | Block retention time on local disk.<br> |
| alertmanagersURLs | []string | No | - | Alertmanager replica URLs to push firing alerts. Ruler claims success if push to at<br>least one alertmanager from discovered succeeds. The scheme should not be empty e.g<br>`http` might be used. The scheme may be prefixed with 'dns+' or 'dnssrv+' to detect<br>Alertmanager IPs through respective DNS lookups. The port defaults to 9093 or the SRV<br>record's value. The URL path is used as a prefix for the regular Alertmanager API path.<br> |
| alertmanagersSendTimeout | string | No | - | Timeout for sending alerts to Alertmanager<br> |
| alertmanagersSDDNSInterval | string | No | - | Interval between DNS resolutions of Alertmanager hosts.<br> |
| alertQueryUrl | string | No | - | The external Thanos Query URL that would be set in all alerts 'Source' field<br> |
| alertLabelDrop | map[string]string | No | - | Labels by name to drop before sending to alertmanager. This allows alert to be<br>deduplicated on replica label (repeated). Similar Prometheus alert relabelling<br> |
| webRoutePrefix | string | No | - | Prefix for API and UI endpoints. This allows thanos UI to be served on a sub-path. This<br>option is analogous to --web.route-prefix of Promethus.<br> |
| webExternalPrefix | string | No | - | Static prefix for all HTML links and redirect URLs in the UI query web interface. Actual<br>endpoints are still served on / or the web.route-prefix. This allows thanos UI to be<br>served behind a reverse proxy that strips a URL sub-path.<br> |
| webPrefixHeader | string | No | - | Name of HTTP request header used for dynamic prefixing of UI links and redirects. This<br>option is ignored if web.external-prefix argument is set. Security risk: enable this<br>option only if a reverse proxy in front of thanos is resetting the header. The<br>--web.prefix-header=X-Forwarded-Prefix option can be useful, for example, if Thanos UI is<br>served via Traefik reverse proxy with PathPrefixStrip option enabled, which sends the<br>stripped prefix value in X-Forwarded-Prefix header. This allows thanos UI to be served on a<br>sub-path.<br> |
| queries | []string | No | - | Addresses of statically configured query API servers (repeatable). The scheme may be<br>prefixed with 'dns+' or 'dnssrv+' to detect query API servers through respective DNS<br>lookups.<br> |
| querySddnsInterval | string | No | - | Interval between DNS resolutions.<br> |
### ThanosStatus
#### ThanosStatus defines the observed state of Thanos

| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
### Thanos
#### Thanos is the Schema for the thanos API

| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
|  | metav1.TypeMeta | Yes | - |  |
| metadata | metav1.ObjectMeta | No | - |  |
| spec | ThanosSpec | No | - |  |
| status | ThanosStatus | No | - |  |
### ThanosList
#### ThanosList contains a list of Thanos

| Variable Name | Type | Required | Default | Description |
|---|---|---|---|---|
|  | metav1.TypeMeta | Yes | - |  |
| metadata | metav1.ListMeta | No | - |  |
| items | []Thanos | Yes | - |  |
