## Commands

Levant supports a number of command line arguments which provide control over the Levant binary. Each command supports the `--help` flag to provide usage assistance.

### Command: `deploy`

`deploy` is the main entry point into Levant for deploying a Nomad job and supports the following flags which should then be proceeded by the Nomad job template you which to deploy. Levant also supports autoloading files by which Levant will look in the current working directory for a `levant.[yaml,yml,tf]` file and a single `*.nomad` file to use for the command actions.

* **-address** (string: "http://localhost:4646") The HTTP API endpoint for Nomad where all calls will be made.

* **-canary-auto-promote** (int: 0) The time period in seconds that Levant should wait for before attempting to promote a canary deployment.

* **-consul-address** (string: "localhost:8500") The Consul host and port to use when making Consul KeyValue lookups for template rendering.

* **-force-batch** (bool: false) Forces a new instance of the periodic job. A new instance will be created even if it violates the job's prohibit_overlap settings.

* **-force-count** (bool: false) Use the taskgroup count from the Nomad job file instead of the count that is obtained from the running job count.

* **-log-level** (string: "INFO") The level at which Levant will log to. Valid values are DEBUG, INFO, WARNING, ERROR and FATAL.

* **-log-format** (string: "HUMAN") Specify the format of Levant's logs. Valid values are HUMAN or JSON

* **-var-file** (string: "") The variables file to render the template with. This flag can be specified multiple times to supply multiple variables files.

The `deploy` command also supports passing variables individually on the command line. Multiple commands can be passed in the format of `-var 'key=value'`. Variables passed via the command line take precedence over the same variable declared within a passed variable file.

Full example:

```
levant deploy -log-level=debug -address=nomad.devoops -var-file=var.yaml -var 'var=test' example.nomad
```

### Dispatch: `dispatch`

`dispatch` allows you to dispatch an instance of a Nomad parameterized job and utilise Levant's advanced job checking features to ensure the job reaches the correct running state.

* **-address** (string: "http://localhost:4646") The HTTP API endpoint for Nomad where all calls will be made.

* **-log-level** (string: "INFO") The level at which Levant will log to. Valid values are DEBUG, INFO, WARNING, ERROR and FATAL.

* **-log-format** (string: "HUMAN") Specify the format of Levant's logs. Valid values are HUMAN or JSON

* **-meta** (string: "key=vaule") The metadata key will be merged into the job's metadata. The job may define a default value for the key which is overridden when dispatching. The flag can be provided more than once to inject multiple metadata key/value pairs. Arbitrary keys are not allowed. The parameterized job must allow the key to be merged.

The command also supports the ability to send data payload to the dispatched instance. This can be provided via stdin by using "-" for the input source or by specifying a path to a file.

Full example:

```
levant dispatch -log-level=debug -address=nomad.devoops -meta key=value dispatch_job payload_item
```

### Command: `render`

`render` allows rendering of a Nomad job template without deploying, useful when testing or debugging. Levant also supports autoloading files by which Levant will look in the current working directory for a `levant.[yaml,yml,tf]` file and a single `*.nomad` file to use for the command actions.

* **-consul-address** (string: "localhost:8500") The Consul host and port to use when making Consul KeyValue lookups for template rendering.

* **-var-file** (string: "") The variables file to render the template with. This flag can be specified multiple times to supply multiple variables files.

* **-output** (string: "") The path to write the rendered template to. The template will be rendered to stdout if this is not set.

Like `deploy`, the `render` command also supports passing variables individually on the command line. Multiple vars can be passed in the format of `-var 'key=value'`. Variables passed via the command line take precedence over the same variable declared within a passed variable file.

Full example:

```
levant render -var-file=var.yaml -var 'var=test' example.nomad
```

### Command: `scale-in`

The `scale-in` command allows the operator to scale a Nomad job and optional task-group within that job in/down in number. This can be helpful particulary in development and testing of new Nomad jobs or resizing.

* **-address** (string: "http://localhost:4646") The HTTP API endpoint for Nomad where all calls will be made.

* **-count** (int: 0) The count by which the job and task groups should be scaled in by. Only one of count or percent can be passed.

* **-log-level** (string: "INFO") The level at which Levant will log to. Valid values are DEBUG, INFO, WARNING, ERROR and FATAL.

* **-log-format** (string: "HUMAN") Specify the format of Levant's logs. Valid values are HUMAN or JSON

* **-percent** (int: 0) A percentage value by which the job and task groups should be scaled in by. Counts will be rounded up, to ensure required capacity is met. Only one of count or percent can be passed.

* **-task-group** (string: "") The name of the task group you wish to target for scaling. If this is not specified, all task groups within the job will be scaled.

Full example:

```
levant scale-in -count 3 -task-group cache example
```

### Command: `scale-out`

The `scale-out` command allows the operator to scale a Nomad job and optional task-group within that job out/up in number. This can be helpful particulary in development and testing of new Nomad jobs or resizing.

* **-address** (string: "http://localhost:4646") The HTTP API endpoint for Nomad where all calls will be made.

* **-count** (int: 0) The count by which the job and task groups should be scaled out by. Only one of count or percent can be passed.

* **-log-level** (string: "INFO") The level at which Levant will log to. Valid values are DEBUG, INFO, WARNING, ERROR and FATAL.

* **-log-format** (string: "HUMAN") Specify the format of Levant's logs. Valid values are HUMAN or JSON

* **-percent** (int: 0) A percentage value by which the job and task groups should be scaled out by. Counts will be rounded up, to ensure required capacity is met. Only one of count or percent can be passed.

* **-task-group** (string: "") The name of the task group you wish to target for scaling. If this is not specified, all task groups within the job will be scaled.

Full example:

```
levant scale-out -percent 30 -task-group cache example
```

### Command: `version`

The `version` command displays build information about the running binary, including the release version.