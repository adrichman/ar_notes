# Splunk Best Practices
_from .conf 2015_

### Have a Local Splunk instance

* create "sandbox" index - 1 day retention
* VM + Splunk?

### btool

* what would the config be if you reloaded/restarted the conf at that moment?
* not the current runtime
* reveals order of precedence of configs
* add it to the PATH so it's easy to reach

### `btool <conf> list <stanza|> <--debug|>`

* use --debug w/ `| grep`

### Search Speed

* Do you know exactly what you need?
* Fast / Smart / Verbose

### Searches

* whitespace
* cosmetics at end (i.e. renames)
* combine multiple renames with `,` and combine rexs (better performance) 
* don't sort early and exclude results
* require fields if necessary `action=*` excludes where action is NULL
* Be specific about sourcetypes/sources etc because new sources could be added to the index later and you may not want to count them
* use __stats__ to create a transaction

    ```
    | stats count by phone, host
    | fields - count
    ```
* `foreach * [ eval <<FIELD>> = '<<FIELD>>' / pow(1024, 3)]`
* coalesce 
* avoid subsearches, use `OR` instead and mark results to differentiate
* __don't use__ `NOT`
* don't do string manipulations for converting time  - use `convert()`
* `metadata` returns info about an index without having to run a search
* `eventcount`
* Snap-To times for scheduled jobs 
    start:`@hour-1hour` finish:`@hour` 
* Realistic alerts - be relative to the data with `stddev` or `percXX` rather than arbitrary theresholds

### Administration

* Separate installs
    * DS -> Master -> IDXC
    * DS -> Deployer -> SHC
* Bootstrap
    - install splunk binaries
    - point to DS/Master/Deployer
    - Download config and purpose config
    - Downlaod app with scripted input
    - _disable local auth (password) file_
    - _disable .ui-login to avoid default password ui_
    
* Global Config
    - disable splunkweb
    - set ports
    - authentication
    - Transparent huge memory pages
    - source control
* Cluster of One
    - Allows replication of old data for when you need it down the line
* Everyone is `user`, capabilities only for `power+` users
* If you log it, you should splunk it
    - If you don't need it in splunk, maybe you don't need to log it
* Forward all instances to indexers
    - All indexes including summary
* _Indent any config that you've edited_
* `max_searches_perc= 90`
* `[indexer_discovery]`
* DMC

