# Simple Builder

A simple Python script to run jobs defined in a JSON file. 

> I am using this program to run simple parallel jobs

## Jobs definition

The following content can be set in _sbuild.json_ file:

```json
{
    "pipeline": "sbuild-test",
    "version": "0.1",
    "log_dir": "logs",
    "jobs": [
        {
            "name": "first ls",
            "exec": "ls /tmp"
        },
        {
            "name": "second ls",
            "exec": "ls /proc"
        }
    ]
}
```

## Features

- Every job has it own log file

- JSON values can be expanded with environment variables, e.g:

  - ```json
    {
        "pipeline": "sbuild-test",
        "version": "$VERSION",
        "log_dir": "logs",
        "jobs": [
            {
                "name": "test",
                "exec": "echo $VERSION"
            }
        ]
    }
    ```

  - Run it as: $ VERSION=0.1 ./sbuild --json sbuild.json

## Example

```bash
$ VERSION=0.1 ./sbuild --json build.json
2020-01-03 12:15:39,399 [    INFO]       Status: starting builder
2020-01-03 12:15:39,399 [    INFO]     Pipeline: sbuild-test
2020-01-03 12:15:39,400 [    INFO]      Version: 0.1
2020-01-03 12:15:39,400 [    INFO]     Logs Dir: logs/sbuild-test/0.1/2020-01-03-12_15_39
2020-01-03 12:15:39,400 [    INFO]        Job 0: first ls
2020-01-03 12:15:39,401 [    INFO]        Job 1: second ls
2020-01-03 12:15:39,403 [    INFO] Status Check: every 1 second(s)
2020-01-03 12:15:39,403 [    INFO]        Job 0: first ls has finished, status code = 0
2020-01-03 12:15:40,404 [    INFO]        Job 1: second ls has finished, status code = 0
2020-01-03 12:15:41,406 [    INFO] Status Check: all jobs have finished (2/2 passed)
```

