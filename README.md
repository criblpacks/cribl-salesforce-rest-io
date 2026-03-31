# Salesforce Rest Collector IO
----

## About this Pack
This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the Pack's context - you can choose how data arrives at a DESTINATION:
*  *Send to Worker Group Routes* (the default): data is sent to the top-level Worker Group Routes.
*  *Default Destination*: data is sent to the Worker Group's [Default Destination](https://docs.cribl.io/stream/destinations-default/). 
*  *In-Pack Destination*: data is sent to one or more Destinations configured within the Pack.

This Cribl Pack is designed to streamline the collection and processing of event log file events from the Salesforce API. It enables efficient extraction of critical event data, such as user activity, system performance, and security events, directly from Salesforce's Event Log Files (ELF). The pack includes pre-configured pipelines, sources, and transformations to authenticate with the Salesforce API, retrieve log file metadata, and ingest event data into your Cribl Stream environment for further analysis, enrichment, or routing. Ideal for organizations looking to monitor Salesforce environments, enhance security observability, or derive operational insights from event data.

Additionally Salesforce objects such as LoginHistory and SetupAuditTrail are included in the collector, additional Objects can be defined as well.

## Deployment

* Every bundled Source within this pack adds a hidden field: `__packsource`. This field allows for simplified routing based on the Pack source.
* This pack is configured by default to use the Destination *Send to Worker Group Routes*. You *must* add either a Worker Group Route or rely on the Default Destination.
* To explicitly use the Worker Group's *Default Destination*, change the Pack's Routes to *default:default*. The Pack will then route the data to the destination currently set as the Default on the Worker Group.

### Configure the Collector
Some configuration items are required for pulling data from the Salesforce API. Navigate to Knowledge > Variables, update the following with your values:

1. Salesforce domain variable - `salesforce_domain`
2. Salesforce API Version variable (if required) - `salesforce_api_version`
3. Salesforce Client ID variable - `salesforce_oauth_clientid`
4. Navigate to Sources > Collectors (REST) > in_salesforce_api within the Pack and update the `Client Secret Value` under `Authentication` with your secret.


Optional Configuration:
- If additional objects from the Salesforce API are needed you can modify the JSON Array under Knowledge > Variables > `salesforce_objects`. Two objects have been configured to start and provide the formatting for how to add additional objects. For information on available objects and fields please reference [Salesforce Objects](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_list.htm).

### Configure your Destination/Update Pack Routes
To ensure proper data routing, you must make a choice: retain the current setting to use the Default Destination defined by your Worker Group, or define a new Destination directly inside this pack and adjust the pack's route accordingly.

### Commit and Deploy
Once everything is configured, perform a Commit & Deploy to enable data collection (if changes have been made).

## Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.

## Release Notes
### Version 2.0.0
* Updated Route Destinations to "Send to Worker Group Routes". See above for details.

### Verison 1.1.2
- Fixed a bug in the Collector preventing OAUTH from working.
- Removed included Splunk HEC Destination

### Version 1.1.0
- Most Collector configuration is now done using variables.

### Version 1.0.0
- Initial release

## Contributing to the Pack

To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.

## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).
