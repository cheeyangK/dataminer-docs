---
uid: General_Main_Release_10.4.0_CU1
---

# General Main Release 10.4.0 CU1 - Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### Circular correlation rules will now be blocked [ID_38301]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

A correlation rule will now be blocked when it was triggered due to a correlated alarm that depends on an alarm created by the rule in question.

> [!NOTE]
> ​This feature only works when the correlation rule and all alarms in question reside on the same DataMiner Agent.

#### Automation: Late script control requests will now be ignored [ID_38409]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

From now on, SLAutomation will ignore any script control request it receives for a script that is not running or not running anymore, and will add an entry in the SLAutomation.txt log file when it does so.

Examples of new log entries:

- DEBUG (5): `Handling script command 'Continue' (2) for script with ID 954.`
- ERROR (-1): `Handling command 'Continue' (2) for script with ID 954 failed with error code 2147942487.`
- ERROR (-1): `Handling command 'Continue' (2) for script with ID 954 failed because it is not interactive.`
- INFO (-1): `Handling command 'Continue' (2) for script with ID 954 failed because it is not active.`

In the latter case, no error would be returned up to now.

#### GQI: All GQI queries opened by the same user will now share one and the same connection [ID_38452]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, each GQI query would open a dedicated SLNet connection. From now on, all GQI queries launched by the same user will share one and the same connection.

#### Enhanced performance when applying a table filter subscription containing wildcards and when applying a partial table cell subscription [ID_38555]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

Because of a number of enhancements, overall performance has increased

- when applying an initial table filter subscription containing wildcards that needs to be handled by the SLElement process, and
- when applying a subscription of a partial table cell.

#### Service & Resource Management: Booking name validation now case-insensitive [ID_38556]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

The validation of the name of a booking is now case-insensitive. This means that when the SRM Framework checks if there are future bookings with the same name, the casing is now no longer taken into account.

#### DataMiner Object Models: GenericEnum values will now be converted to the display value prior to being used in a DOM instance name concatenation [ID_38586]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

The `DomInstanceNameDefinition` class contains a simple list of `IDomInstanceConcatenationItems`. With this, you can add concatenation items of two types in a specific order to define your name: `StaticValueConcatenationItem` or `FieldValueConcatenationItem`.

In the case of the latter, if a `FieldValue` contains data for a `GenericEnumFieldDescriptor` (which can be either string values or integer values), these values will now be converted to the display value.

> [!NOTE]
> Currently, using `GenericEnum` fields containing multiple values are not supported for name concatenation.

#### SLAnalytics - Behavioral anomaly detection: Suggestion event generation will now be limited [ID_38674]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

From now on, the generation of anomaly suggestion events will be limited to 50 events per hour per type of anomaly (level shift, trend change, flatline or variance change).

> [!NOTE]
> The generation of anomaly alarm events (i.e. on parameters that have anomaly monitoring configured in the alarm template) will remain unlimited.

#### GQI: Clearer error message will now be thrown when an ad hoc data source or custom operator cannot be instantiated [ID_38686]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, when an ad hoc data source or custom operator could not be instantiated, the following exception would be thrown when an error occurred on object creation level (within the constructor):

`Error: Could not create instance of datasource when trying to use an ad hoc datasource.`

From now on, the following exception will be thrown instead:

`Error trapped: Could not create instance of datasource 'datasource ID': <exception message>.`

\* `<exception message>` being the message that was thrown within the constructor.

#### SLLogCollector will now also collect the logs of the CommunicationGateway DxM [ID_38716]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

SLLogCollector will now also collect the logs of the *CommunicationGateway* DxM.

#### Security enhancements [ID_38756] [ID_38650]

<!-- RN 38756: MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->
<!-- RN 38650: MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

A number of security enhancements have been made.

#### SLAnalytics - Trend predictions: Enhanced accuracy of the trend prediction mechanism [ID_38767]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

Because of a number of enhancements, overall accuracy of the trend prediction mechanism has been improved.

#### SLProtocol will no longer forward all changes to standalone parameters to SLElement [ID_38785]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, SLProtocol would forward all changes to standalone parameters to SLElement, even when this was not strictly necessary. From now on, SLProtocol will only forward changes to standalone parameters to SLElement when the latter requires them.

Also, when an SNMP parameter used a wildcard as OID, up to now, SLProtocol would forward the value of that wildcard to SLElement, which would then pass it on to the SLSNMPManager process. From now on, SLProtocol will forward those wildcard values directly to SLSNMPManager.

#### Service & Resource Management: Past bookings will no longer be queried when creating a new booking or calculating available resources [ID_38798]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

When creating or updating a booking, up to now, overlapping past bookings would be queried. This was necessary to validate the usage of contributing bookings that had already ended. In order to avoid the retrieval of those past bookings, the behavior of contributing bookings has now been altered.

From now on, it will no longer be possible to reuse a contributing booking that has already ended in a new booking. However, updating an existing main booking that uses a contributing booking will still be possible.

#### At installation the StorageModule service will now be configured to restart itself after each failure [ID_38843]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

At installation, the StorageModule service will now be configured to restart itself after each failure.

#### At installation the APIGateway service will now be configured to restart itself after each failure [ID_38855]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

At installation, the APIGateway service will now be configured to restart itself after each failure.

#### GQI: Full logging [ID_38870]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

Full GQI logging will now be available in the `C:\Skyline DataMiner\Logging\GQI` folder.

The log level can be configured in the `<appSettings>` element of the `C:\Skyline DataMiner\Files\SLHelper.exe.config` file.

By default, this file will contain the following GQI log settings:

```xml
<add key="serilog:minimum-level" value="Information" />
```

In case of issues that need investigating, you can temporarily lower the minimum log level to "Debug".

> [!NOTE]
>
> - The *SLHelper.exe.config* file is overwritten with the default configuration during full DataMiner upgrades or downgrades.
> - A GQI error log will be added in the `C:\Skyline DataMiner\Logging\GQI` folder for every GQI request that fails.

#### SLAnalytics - Behavioral anomaly detection: Enhanced generation of suggestion events when detecting variance changes [ID_38941]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

A number of enhancements have been made to the mechanism that automatically generates a suggestion event when a variance change is detected.

### Fixes

#### SLLogCollector: Minor issues [ID_38011]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

A number of minor issues were fixed with regard to the SLLogCollector tool.

#### Problem when a redundancy group was set to an undefined state [ID_38401]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When a redundancy group was set to an undefined state, a large number of empty connectivity contexts would be inserted into the *Connectivity* section of the *redundancy.xml* file. As a result, the correct connectivity contexts would be overwritten, causing the redundancy group to be stuck in the undefined state.

#### Problem with file offload mechanism when main database is offline [ID_38542]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When the main database is offline, file offloads are used to store write/delete operations. In some cases, this file offload mechanism could end up in an unrecoverable state due to a threading issue.

#### Hostname of SNMP element would not get resolved after the element had gone into timeout [ID_38547]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When an element with an SNMP connection that was configured with a hostname instead of an IP address went into timeout, and during the timeout the hostname could not be resolved, the element would remain in timeout and would no longer try to resolve the hostname until it was restarted.

Also, in StreamViewer, the error messages that indicate that the hostname could not be resolved have now been made clearer. For example, in case of SNMPv3, a generic `DISCOVERY FAILED` error would appear when something went wrong while setting up a connection. From now on, the error will indicate what exactly went wrong (e.g. the engine ID could not be discovered, the user credentials were not valid, etc.).

#### SLAnalytics - Pattern matching: A match of one subpattern would incorrectly be considered a match of the entire multivariate pattern [ID_38587]

<!-- MR 10.4.0 [CU1] - FR 10.4.3 -->

When the streaming method was being used, a match detected for one subpattern of a multivariate pattern would incorrectly be considered a match of that entire multivariate pattern.

Although the suggestion events were generated correctly, the pattern matches would not be indicated correctly on the trend graphs.

#### Problem with SLProtocol when calculating the length of a serial response [ID_38591]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

In some cases, SLProtocol could stop working due to an `Access violation reading location` error being thrown while calculating the length of a serial response.

#### GQI: Problem when sorting DOM instances when the column by which you sorted contained null values [ID_38592]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When DOM instances were sorted, in some cases, an error could be thrown when the column by which you sorted contained null values.

#### Problem when a DataMiner Cube client tried to connect using gRPC [ID_38606]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When a DataMiner Cube client tried to connect to a DataMiner Agent using gRPC, in some rare cases, a disconnect could occur with the following error:

`Some messages have probably gone lost. Waiting for X while X+20 already entered.`

#### SLAnalytics - Automatic incident tracking: Problem when updating alarm groups [ID_38629]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

Each time the focus score of an alarm is updated, incident tracking has to update its alarm groups. In some cases, incident tracking would incorrectly update its groups twice, causing the groups to be set to an undefined state.

#### DaaS: The StorageModule service would incorrectly start up before the NATS service had started up [ID_38644]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

When starting a DaaS system (DataMiner as a Service), in some cases, the StorageModule service would start up before the NATS service had started up. As a result, StorageModule would fail to connect to NATS and would shut down.

The DaaS startup routine has now been improved to prevent issues like the one described above.

#### Service & Resource Management: Booking corrupted after SRM_QuarantineHandling retrieved incorrect version of the booking [ID_38646]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, it could occur that the script *SRM_QuarantineHandling* retrieved a previous version of a booking instead of the latest, quarantined version, which could cause subsequent updates to corrupt the booking object. To prevent this, *SRM_QuarantineHandling* will now be called after a booking is saved.

#### SLAnalytics - Behavioral anomaly detection: Problem when updating the anomaly configuration for a DVE element [ID_38661]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

When you had updated the anomaly configuration for a DVE element, SLAnalytics would not process the changes correctly, causing incorrect behavioral anomaly alarms to be generated.

#### DataMiner upgrade: Some folders would not get cleaned up when performing an upgrade [ID_38672]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, the following folders would incorrectly not get cleaned up when performing a DataMiner upgrade:

- `C:\Skyline DataMiner\Webpages\API\bin`
- `C:\Skyline DataMiner\Webpages\Maps\bin`

#### Errors would be thrown at DataMiner startup when production protocols had an information template assigned [ID_38683]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

At DataMiner startup, in some cases, errors could incorrectly be thrown when at least one production protocol had an information template assigned.

#### SLAnalytics: Problem when processing an element with an invalid alarm template [ID_38724]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

In some cases, SLAnalytics could stop working while processing an element with an invalid alarm template.

#### Paused element set back to the active state would no longer receive any alarm updates [ID_38744]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When a paused element was set back to the "started" state, it would no longer receive any alarm updates until it was restarted.

#### DataMiner Maps: KML layers would incorrectly always be displayed first in the legend [ID_38746]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When using either Google Maps or OpenStreetMap, KML layers would incorrectly always be displayed first in the layer legend, regardless of the order in which they were specified in the map configuration file.

From now on, the legend will always show the layers in the order in which they were specified in the map configuration file.

#### Failover: Memory leak when invoking PowerShell scripts [ID_38763]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

On Failover systems using a shared hostname, SLNet regularly executes PowerShell scripts. However, invoking those scripts would cause a memory leak. To prevent this, each PowerShell script will now be run in a separate process, which will be terminated at the end of the script.

#### Automation: Problem when sending an email to a user or group [ID_38844]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When an Automation script sent an email to a user or a user group using an *Email* action, in some cases, an error could be thrown.

#### Problem with SLProtocol when it took longer than 15 minutes to execute a poll group [ID_38858]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When an element used SNMP or HTTP communication, a notification would only be sent to SLWatchdog when a poll group finished executing. As a result, when it took longer than 15 minutes to execute a poll group, an SLProtocol run-time error alarm would be generated and subsequently cleared when the poll group finished.

In order to avoid such run-time error alarms from being generated, a check will now be performed when a response is received, and an additional notification will be sent to SLWatchdog when the first notification to SLWatchdog was sent more than one minute ago.

#### STaaS: Failing request would not be retried [ID_38874]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

When a request to the cloud failed, in some cases, the Azure SDK would not be able to perform any retries and would throw the following exception:

`System.ArgumentOutOfRangeException: 'minValue' cannot be greater than maxValue.`

#### Mediation protocols: Problem when the value of the 'baseFor' attribute is identical to that of the '\<ElementType\>' tag [ID_38878]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When a mediation protocol had a `baseFor` attribute with a value identical to that of its `<ElementType>` tag, this could lead to issues in SLNet.

From now on, it will no longer be possible to upload a protocol of which the value of the `baseFor` attribute is identical to that of the `<ElementType>` tag.

#### STaaS: Problem when generating a DataMiner backup with the database backup option enabled [ID_38896]

<!-- MR 10.4.0 [CU1] - FR 10.4.4 -->

Up to now, on STaaS systems, a notice would be generated when a DataMiner backup was executed with the database backup option enabled.

From now on, when a DataMiner backup is executed with the database backup option enabled, on a STaaS system, no database backup will be performed.

> [!NOTE]
> On STaaS systems, database backups are taken automatically. If you want a STaaS backup to be restored, contact [Skyline support](mailto:techsupport@skyline.be).

#### Problem with SLLog when stopping or restarting DataMiner [ID_38902]

<!-- MR 10.3.0 [CU13] / 10.4.0 [CU1] - FR 10.4.4 -->

When DataMiner was stopped or restarted, in some cases, the SLLog process could stop working.

#### SLAnalytics will no longer automatically restore a lost session with SLDataGateway [ID_38984]

<!-- MR 10.3.0 [CU14] / 10.4.0 [CU1] - FR 10.4.4 -->

Since DataMiner version 10.3.0 [CU9]/10.3.12, SLAnalytics would automatically restore a lost session with SLDataGateway. From now on, it will no longer do so.
