# scale-ci-diagnosis

Tool to help diagonize issues with OpenShift clusters. It does it by:
- capturing prometheus DB from the running prometheus pods to local file system. This can be used to look at the metrics later by running prometheus locally with the backed up DB.

## Run
```
Edit env.sh according to the needs and run the ocp_diagnosis script:

$ source env.sh; ./ocp_diagnosis.sh

options supported:
	 OUTPUT_DIR=str,                       str=dir to store the capture prometheus data
	 PROMETHEUS_CAPTURE=str,               str=true or false, enables/disables prometheus capture
	 PROMETHEUS_CAPTURE_TYPE=str,          str=wal or full, wal captures the write ahead log and full captures the entire prometheus DB
```

## Visualize the captured data locally on prometheus server
```
$ ./prometheus_view.sh <db_tarball_url>
```
This installs prometheus server and loads up the DB, the server can be accessed at https://localhost:9090.
