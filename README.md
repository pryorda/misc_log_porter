misc_log_porter: Export logs from any filesystem
==============================
This container is based on the balabit/syslog-ng image and has the sole purpose of exporting logs from a shared volume or filesystem.

#### Build
Steps to build this image:
```
docker build -t misc_log_porter .
```

#### Test
Testing this image is pretty simple:
```
docker run --rm --name misc_log_porter -d -v ${PWD}/test:/var/log/test -v syslog-persist:/var/lib/syslog-ng/ misc_log_porter
./test_logs.sh
docker logs misc_log_porter
docker stop misc_log_porter
docker volume rm syslog-persist
```

#### Usage
To run this image with with persistent data, base_dir, and log_pattern, run the following: 
```
docker run -d -v ${PWD}/test:/var/log/test -e BASE_DIR=/var/log/test -e LOG_PATTERN='*log' -e RECURSIVE=no -v syslog-persist:/var/lib/syslog-ng/ misc_log_porter
```
#### Environment Variables
| varible      | default  | description                                      |
| ------------ | -------- | ------------------------------------------------ |
| `LOG_PATTERN`| *log     | Syslog-ng wildcard-file pattern: Refer to docs   |
| `BASE_DIR`   | /var/log | This is the directory syslog will be searching against the pattern |
| `RECURSIVE`  | no       | Recursively look in child directories (yes or no)|

#### Maintainer

Daniel Pryor [pryorda](https://github.com/pryorda)