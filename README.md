# scale-ci-diagnosis

Tool to help diagonize issues with OpenShift clusters. It does it by:
- capturing prometheus DB from the running prometheus pods to local file system. This can be used to look at the metrics later by running prometheus locally with the backed up DB.
- Capturing openshift cluster information including  all the operator managed components using https://github.com/openshift/must-gather.

## Run
```
Edit env.sh according to the needs and run the ocp_diagnosis script:

$ source env.sh; ./ocp_diagnosis.sh

options supported:
	OUTPUT_DIR=str,                       str=dir to store the capture prometheus data
	PROMETHEUS_CAPTURE=str,               str=true or false, enables/disables prometheus capture
	PROMETHEUS_CAPTURE_TYPE=str,          str=wal or full, wal captures the write ahead log and full captures the entire prometheus DB
	OPENSHIFT_MUST_GATHER=str,            str=true or false, gathers cluster data including information about all the operator managed components
	STORAGE_MODE=str,                     str=pbench, moves the results to the pbench results dir to be shipped to the pbench server in case the tool is run using pbench
```

### Pbench server for storage
[Pbench](https://github.com/distributed-system-analysis/pbench.git) does a great job in terms of both collection and long term storage. The tool currently supports pbench as the storage mode instead of just storing the results on the local file system, we will be adding support to store results in Amazon S3 in the future.

In order to use pbench as the storage, the tool needs to be run using pbench and STORAGE_MODE should be set to pbench:

```
$ source env.sh; pbench-user-benchmark --sysinfo=none ocp_diagnosis.sh
# pbench-move-results --prefix ocp-diagnosis-$(date +"%Y%m%d-%H%M%S")
```

## Visualize the captured data locally on prometheus server
```
$ ./prometheus_view.sh <db_tarball_url>
```
This installs prometheus server and loads up the DB, the server can be accessed at https://localhost:9090.
