# Git maintenance

Run tasks to optimize Git repository data.

Run tasks to optimize Git repository data, speeding up other Git commands and reducing storage requirements for the repository.

Git commands that add repository data, such as git add or git fetch, are optimized for a responsive user experience. These commands do not take time to optimize the Git data, since such optimizations scale with the full size of the repository while these user commands each perform a relatively small action.

The git maintenance command provides flexibility for how to optimize the Git repository.

## Options

### run

Run one or more maintenance tasks. If one or more --task options are specified, then those tasks are run in that order. Otherwise, the tasks are determined by which maintenance.<task>.enabled config options are true. By default, only maintenance.gc.enabled is true.

### start

Start running maintenance on the current repository. This performs the same config updates as the register subcommand, then updates the background scheduler to run git maintenance run --scheduled on an hourly basis.

### stop

Halt the background maintenance schedule. The current repository is not removed from the list of maintained repositories, in case the background maintenance is restarted later.

```
--schedule
```

When combined with the run subcommand, run maintenance tasks only if certain time conditions are met, as specified by the maintenance.<task>.schedule config value for each <task>. This config value specifies a number of seconds since the last time that task ran, according to the maintenance.<task>.lastRun config value. The tasks that are tested are those provided by the --task=<task> option(s) or those with maintenance.<task>.enabled set to true.

## Specific tasks

[Specific tasks](https://git-scm.com/docs/git-maintenance#_tasks)
