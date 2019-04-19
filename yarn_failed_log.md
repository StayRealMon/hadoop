# master： #
**hadoop-root-namenode-ubuntu1.log**
**hadoop-root-secondarynamenode-ubuntu1.log**
**yarn-root-resourcemanager-ubuntu1.log**


# worker2： #
**hadoop-root-datanode-ubuntu2.log **

> 2019-03-20 22:46:54,025 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Creating a new application reference for app application_1553147085057_0001
2019-03-20 22:46:54,035 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from NEW to INITING
2019-03-20 22:46:54,035 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.141      OPERATION=Start Container Request       TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000001
2019-03-20 22:46:54,036 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Adding container_1553147085057_0001_01_000001 to application application_1553147085057_0001
2019-03-20 22:46:54,040 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from INITING to RUNNING
2019-03-20 22:46:54,045 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000001 transitioned from NEW to LOCALIZING
2019-03-20 22:46:54,045 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_INIT for appId application_1553147085057_0001
2019-03-20 22:46:54,054 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.splitmetainfo transitioned from INIT to DOWNLOADING
2019-03-20 22:46:54,054 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.jar transitioned from INIT to DOWNLOADING
2019-03-20 22:46:54,054 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.split transitioned from INIT to DOWNLOADING
2019-03-20 22:46:54,054 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.xml transitioned from INIT to DOWNLOADING
2019-03-20 22:46:54,055 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.ResourceLocalizationService: Created localizer for container_1553147085057_0001_01_000001
2019-03-20 22:46:54,146 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.ResourceLocalizationService: Writing credentials to the nmPrivate file /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/nmPrivate/container_1553147085057_0001_01_000001.tokens. Credentials list:
2019-03-20 22:46:54,171 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Initializing user root
2019-03-20 22:46:54,194 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Copying from /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/nmPrivate/container_1553147085057_0001_01_000001.tokens to /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000001.tokens
2019-03-20 22:46:54,195 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Localizer CWD set to /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001 = file:/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001
2019-03-20 22:46:54,924 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.splitmetainfo(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/10/job.splitmetainfo) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:46:54,966 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.jar(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/11/job.jar) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:46:54,996 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.split(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/12/job.split) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:46:55,027 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.xml(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/13/job.xml) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:46:55,029 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000001 transitioned from LOCALIZING to LOCALIZED
2019-03-20 22:46:55,054 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000001 transitioned from LOCALIZED to RUNNING
2019-03-20 22:46:55,059 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: launchContainer: [bash, /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000001/default_container_executor.sh]
2019-03-20 22:46:55,641 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Starting resource-monitoring for container_1553147085057_0001_01_000001
2019-03-20 22:46:55,706 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 7197 for container-id container_1553147085057_0001_01_000001: 59.3 MB of 1.5 GB physical memory used; 2.6 GB of 3.1 GB virtual memory used
2019-03-20 22:46:58,746 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 7197 for container-id container_1553147085057_0001_01_000001: 231.5 MB of 1.5 GB physical memory used; 2.6 GB of 3.1 GB virtual memory used
.................................
2019-03-20 22:48:32,821 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 7197 for container-id container_1553147085057_0001_01_000001: 368.8 MB of 1.5 GB physical memory used; 2.7 GB of 3.1 GB virtual memory used
2019-03-20 22:48:35,779 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Container container_1553147085057_0001_01_000001 succeeded
2019-03-20 22:48:35,779 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000001 transitioned from RUNNING to EXITED_WITH_SUCCESS
2019-03-20 22:48:35,780 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Cleaning up container container_1553147085057_0001_01_000001
2019-03-20 22:48:35,842 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 7197 for container-id container_1553147085057_0001_01_000001: -1B of 1.5 GB physical memory used; -1B of 3.1 GB virtual memory used
2019-03-20 22:48:35,935 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Deleting absolute path : /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000001
2019-03-20 22:48:35,935 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root OPERATION=Container Finished - Succeeded        TARGET=ContainerImpl    RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000001
2019-03-20 22:48:35,939 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000001 transitioned from EXITED_WITH_SUCCESS to DONE
2019-03-20 22:48:35,940 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Removing container_1553147085057_0001_01_000001 from application application_1553147085057_0001
2019-03-20 22:48:35,941 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_STOP for appId application_1553147085057_0001
2019-03-20 22:48:36,506 INFO SecurityLogger.org.apache.hadoop.ipc.Server: Auth successful for appattempt_1553147085057_0001_000001 (auth:SIMPLE)
2019-03-20 22:48:36,517 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Stopping container with container Id: container_1553147085057_0001_01_000001
2019-03-20 22:48:36,517 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.141      OPERATION=Stop Container Request        TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000001
2019-03-20 22:48:36,945 INFO org.apache.hadoop.yarn.server.nodemanager.NodeStatusUpdaterImpl: Removed completed containers from NM context: [container_1553147085057_0001_01_000001]
2019-03-20 22:48:36,947 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from RUNNING to APPLICATION_RESOURCES_CLEANINGUP


**yarn-root-nodemanager-ubuntu2.log**
2019-03-20 22:48:36,947 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Deleting absolute path : /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001
2019-03-20 22:48:36,948 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event APPLICATION_STOP for appId application_1553147085057_0001
2019-03-20 22:48:36,951 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from APPLICATION_RESOURCES_CLEANINGUP to FINISHED
2019-03-20 22:48:36,951 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.loghandler.NonAggregatingLogHandler: Scheduling Log Deletion for application: application_1553147085057_0001, with delay of 10800 seconds
2019-03-20 22:48:38,844 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Stopping resource-monitoring for container_1553147085057_0001_01_000001
2019-03-20 23:12:01,260 ERROR org.apache.hadoop.yarn.server.nodemanager.NodeManager: RECEIVED SIGNAL 15: SIGTERM
2019-03-20 23:12:01,276 INFO org.mortbay.log: Stopped HttpServer2$SelectChannelConnectorWithSafeStartup@0.0.0.0:8042
2019-03-20 23:12:01,380 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Applications still running : [application_1553147085057_0001]
2019-03-20 23:12:01,380 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Waiting for Applications to be Finished
2019-03-20 23:12:05,383 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Done waiting for Applications to be Finished. Still alive: [application_1553147085057_0001]
2019-03-20 23:12:05,384 INFO org.apache.hadoop.ipc.Server: Stopping server on 52082
2019-03-20 23:12:05,385 INFO org.apache.hadoop.ipc.Server: Stopping IPC Server listener on 52082
2019-03-20 23:12:05,386 INFO org.apache.hadoop.ipc.Server: Stopping IPC Server Responder

**userlogs/application_1553147085057_00011/container_1553147085057_0001_01_000001/stderr stdout syslog**

**stderr**
> Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory register
INFO: Registering org.apache.hadoop.mapreduce.v2.app.webapp.JAXBContextResolver as a provider class
Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory register
INFO: Registering org.apache.hadoop.yarn.webapp.GenericExceptionHandler as a provider class
Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory register
INFO: Registering org.apache.hadoop.mapreduce.v2.app.webapp.AMWebServices as a root resource class
Mar 20, 2019 10:46:59 PM com.sun.jersey.server.impl.application.WebApplicationImpl _initiate
INFO: Initiating Jersey application, version 'Jersey: 1.9 09/02/2011 11:17 AM'
Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory getComponentProvider
INFO: Binding org.apache.hadoop.mapreduce.v2.app.webapp.JAXBContextResolver to GuiceManagedComponentProvider with the scope "Singleton"
Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory getComponentProvider
INFO: Binding org.apache.hadoop.yarn.webapp.GenericExceptionHandler to GuiceManagedComponentProvider with the scope "Singleton"
Mar 20, 2019 10:46:59 PM com.sun.jersey.guice.spi.container.GuiceComponentProviderFactory getComponentProvider
INFO: Binding org.apache.hadoop.mapreduce.v2.app.webapp.AMWebServices to GuiceManagedComponentProvider with the scope "PerRequest"
log4j:WARN No appenders could be found for logger (org.apache.hadoop.ipc.Server).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.

**syslog**

> 2019-03-20 22:47:00,093 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: job_1553147085057_0001Job Transitioned from INITED to SETUP
2019-03-20 22:47:00,095 INFO [CommitterEvent Processor #0] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: JOB_SETUP
2019-03-20 22:47:00,104 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: job_1553147085057_0001Job Transitioned from SETUP to RUNNING
2019-03-20 22:47:00,118 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu2 to /default-rack
2019-03-20 22:47:00,119 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:00,121 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000000 Task Transitioned from NEW to SCHEDULED
2019-03-20 22:47:00,121 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu2 to /default-rack
2019-03-20 22:47:00,121 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:00,121 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000001 Task Transitioned from NEW to SCHEDULED
2019-03-20 22:47:00,122 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_r_000000 Task Transitioned from NEW to SCHEDULED
2019-03-20 22:47:00,122 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from NEW to UNASSIGNED
2019-03-20 22:47:00,123 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from NEW to UNASSIGNED
2019-03-20 22:47:00,123 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_r_000000_0 TaskAttempt Transitioned from NEW to UNASSIGNED
2019-03-20 22:47:00,125 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: mapResourceRequest:<memory:1024, vCores:1>
2019-03-20 22:47:00,133 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: reduceResourceRequest:<memory:1024, vCores:1>
2019-03-20 22:47:00,172 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Event Writer setup for JobId: job_1553147085057_0001, File: hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job_1553147085057_0001_1.jhist
2019-03-20 22:47:01,066 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:2 ScheduledReds:0 AssignedMaps:0 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:0 ContRel:0 HostLocal:0 RackLocal:0
2019-03-20 22:47:01,953 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1553147085057_0001: ask=4 release= 0 newContainers=0 finishedContainers=0 resourcelimit=<memory:1536, vCores:15> knownNMs=2
2019-03-20 22:47:01,954 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:1536, vCores:15>
2019-03-20 22:47:01,954 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:02,966 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Got allocated containers 1
2019-03-20 22:47:02,968 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned container container_1553147085057_0001_01_000002 to attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:02,969 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:02,969 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:02,970 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:1 ScheduledMaps:1 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
2019-03-20 22:47:03,179 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:03,194 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: The job-jar file on the remote FS is hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.jar
2019-03-20 22:47:03,200 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: The job-conf file on the remote FS is /tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.xml
2019-03-20 22:47:03,201 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Adding #0 tokens and #1 secret keys for NM use for launching container
2019-03-20 22:47:03,201 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Size of containertokens_dob is 1
2019-03-20 22:47:03,202 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Putting shuffle token in serviceData
2019-03-20 22:47:03,242 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from UNASSIGNED to ASSIGNED
 2019-03-20 22:47:03,245 INFO [ContainerLauncher #0] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_LAUNCH for container container_1553147085057_0001_01_000002 taskAttempt attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:03,247 INFO [ContainerLauncher #0] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Launching attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:03,249 INFO [ContainerLauncher #0] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:03,566 INFO [ContainerLauncher #0] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Shuffle port returned by ContainerManager for attempt_1553147085057_0001_m_000000_0 : 13562
2019-03-20 22:47:03,567 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: TaskAttempt: [attempt_1553147085057_0001_m_000000_0] using containerId: [container_1553147085057_0001_01_000002 on NM: [ubuntu3:57320]
2019-03-20 22:47:03,571 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from ASSIGNED to RUNNING
2019-03-20 22:47:03,571 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000000 Task Transitioned from SCHEDULED to RUNNING
2019-03-20 22:47:03,974 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1553147085057_0001: ask=4 release= 0 newContainers=0 finishedContainers=0 resourcelimit=<memory:512, vCores:14> knownNMs=2
2019-03-20 22:47:03,974 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:03,974 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:04,977 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:04,977 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:05,983 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:05,983 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:14,023 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:14,023 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:15,030 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:15,031 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:16,034 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:16,034 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:17,045 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1553147085057_0001_01_000002
2019-03-20 22:47:17,046 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Got allocated containers 1
2019-03-20 22:47:17,046 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1553147085057_0001_m_000000_0:
2019-03-20 22:47:17,062 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned container container_1553147085057_0001_01_000004 to attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:17,062 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:17,062 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:17,062 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:2 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:47:17,075 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from RUNNING to FAIL_CONTAINER_CLEANUP
2019-03-20 22:47:17,075 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:17,076 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from UNASSIGNED to ASSIGNED
2019-03-20 22:47:17,077 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1553147085057_0001_01_000002 taskAttempt attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:17,077 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:17,078 INFO [ContainerLauncher #1] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:17,078 INFO [ContainerLauncher #2] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_LAUNCH for container container_1553147085057_0001_01_000004 taskAttempt attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:17,079 INFO [ContainerLauncher #2] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Launching attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:17,080 INFO [ContainerLauncher #2] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:17,080 INFO [ContainerLauncher #2] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:17,098 INFO [ContainerLauncher #2] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Shuffle port returned by ContainerManager for attempt_1553147085057_0001_m_000001_0 : 13562
2019-03-20 22:47:17,099 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: TaskAttempt: [attempt_1553147085057_0001_m_000001_0] using containerId: [container_1553147085057_0001_01_000004 on NM: [ubuntu3:57320]
2019-03-20 22:47:17,099 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from ASSIGNED to RUNNING
2019-03-20 22:47:17,099 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000001 Task Transitioned from SCHEDULED to RUNNING
2019-03-20 22:47:17,135 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from FAIL_CONTAINER_CLEANUP to FAIL_TASK_CLEANUP
2019-03-20 22:47:17,135 INFO [CommitterEvent Processor #1] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: TASK_ABORT
2019-03-20 22:47:17,212 WARN [CommitterEvent Processor #1] org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter: Could not delete hdfs://master:9000/user/root/QuasiMonteCarlo_1553147208333_203828452/out/_temporary/1/_temporary/attempt_1553147085057_0001_m_000000_0
2019-03-20 22:47:17,213 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_0 TaskAttempt Transitioned from FAIL_TASK_CLEANUP to FAILED
2019-03-20 22:47:17,219 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu2 to /default-rack
2019-03-20 22:47:17,220 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:17,220 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: 1 failures on node ubuntu3
2019-03-20 22:47:17,222 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_1 TaskAttempt Transitioned from NEW to UNASSIGNED
2019-03-20 22:47:17,222 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Added attempt_1553147085057_0001_m_000000_1 to list of failed maps
2019-03-20 22:47:18,063 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:1 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:2 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:47:18,078 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1553147085057_0001: ask=5 release= 0 newContainers=0 finishedContainers=0 resourcelimit=<memory:512, vCores:14> knownNMs=2
2019-03-20 22:47:18,078 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:18,078 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:19,083 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:19,083 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:20,086 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:20,086 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:21,093 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:21,093 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:26,366 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:26,366 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:27,370 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:27,370 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:28,375 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1553147085057_0001_01_000004
2019-03-20 22:47:28,375 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Got allocated containers 1
2019-03-20 22:47:28,375 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigning container Container: [ContainerId: container_1553147085057_0001_01_000006, NodeId: ubuntu3:57320, NodeHttpAddress: ubuntu3:8042, Resource: <memory:1024, vCores:1>, Priority: 5, Token: Token { kind: ContainerToken, service: 192.168.213.143:57320 }, ] to fast fail map
2019-03-20 22:47:28,375 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned from earlierFailedMaps
2019-03-20 22:47:28,375 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1553147085057_0001_m_000001_0:
2019-03-20 22:47:28,375 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from RUNNING to FAIL_CONTAINER_CLEANUP
2019-03-20 22:47:28,376 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned container container_1553147085057_0001_01_000006 to attempt_1553147085057_0001_m_000000_1
2019-03-20 22:47:28,376 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:28,376 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:28,376 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:3 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:47:28,376 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:28,376 INFO [ContainerLauncher #3] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1553147085057_0001_01_000004 taskAttempt attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:28,376 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_1 TaskAttempt Transitioned from UNASSIGNED to ASSIGNED
2019-03-20 22:47:28,378 INFO [ContainerLauncher #3] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:28,378 INFO [ContainerLauncher #3] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:28,434 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_LAUNCH for container container_1553147085057_0001_01_000006 taskAttempt attempt_1553147085057_0001_m_000000_1
2019-03-20 22:47:28,434 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Launching attempt_1553147085057_0001_m_000000_1
2019-03-20 22:47:28,434 INFO [ContainerLauncher #4] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:47:28,444 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from FAIL_CONTAINER_CLEANUP to FAIL_TASK_CLEANUP
2019-03-20 22:47:28,444 INFO [CommitterEvent Processor #2] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: TASK_ABORT
2019-03-20 22:47:28,459 WARN [CommitterEvent Processor #2] org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter: Could not delete hdfs://master:9000/user/root/QuasiMonteCarlo_1553147208333_203828452/out/_temporary/1/_temporary/attempt_1553147085057_0001_m_000001_0
2019-03-20 22:47:28,459 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_0 TaskAttempt Transitioned from FAIL_TASK_CLEANUP to FAILED
2019-03-20 22:47:28,460 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu2 to /default-rack
2019-03-20 22:47:28,460 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:47:28,461 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_1 TaskAttempt Transitioned from NEW to UNASSIGNED
2019-03-20 22:47:28,461 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: 2 failures on node ubuntu3
2019-03-20 22:47:28,462 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Added attempt_1553147085057_0001_m_000001_1 to list of failed maps
2019-03-20 22:47:28,466 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Shuffle port returned by ContainerManager for attempt_1553147085057_0001_m_000000_1 : 13562
2019-03-20 22:47:28,466 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: TaskAttempt: [attempt_1553147085057_0001_m_000000_1] using containerId: [container_1553147085057_0001_01_000006 on NM: [ubuntu3:57320]
2019-03-20 22:47:28,466 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_1 TaskAttempt Transitioned from ASSIGNED to RUNNING
2019-03-20 22:47:29,377 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:1 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:3 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:47:29,380 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1553147085057_0001: ask=1 release= 0 newContainers=0 finishedContainers=0 resourcelimit=<memory:512, vCores:14> knownNMs=2
2019-03-20 22:47:29,380 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:29,380 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:47:30,385 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:47:30,385 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:48:27,590 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:48:27,590 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:48:28,599 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1553147085057_0001_01_000014
2019-03-20 22:48:28,600 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Got allocated containers 1
2019-03-20 22:48:28,600 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigning container Container: [ContainerId: container_1553147085057_0001_01_000016, NodeId: ubuntu3:57320, NodeHttpAddress: ubuntu3:8042, Resource: <memory:1024, vCores:1>, Priority: 5, Token: Token { kind: ContainerToken, service: 192.168.213.143:57320 }, ] to fast fail map
2019-03-20 22:48:28,600 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1553147085057_0001_m_000000_3:
2019-03-20 22:48:28,600 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_3 TaskAttempt Transitioned from RUNNING to FAIL_CONTAINER_CLEANUP
2019-03-20 22:48:28,600 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned from earlierFailedMaps
2019-03-20 22:48:28,601 INFO [ContainerLauncher #3] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1553147085057_0001_01_000014 taskAttempt attempt_1553147085057_0001_m_000000_3
2019-03-20 22:48:28,601 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Assigned container container_1553147085057_0001_01_000016 to attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,602 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=<memory:512, vCores:14>
2019-03-20 22:48:28,602 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold not met. completedMapsForReduceSlowstart 1
2019-03-20 22:48:28,602 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:8 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:48:28,602 INFO [ContainerLauncher #3] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1553147085057_0001_m_000000_3
2019-03-20 22:48:28,602 INFO [ContainerLauncher #3] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:48:28,602 INFO [AsyncDispatcher event handler] org.apache.hadoop.yarn.util.RackResolver: Resolved ubuntu3 to /default-rack
2019-03-20 22:48:28,603 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_3 TaskAttempt Transitioned from UNASSIGNED to ASSIGNED
2019-03-20 22:48:28,603 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_LAUNCH for container container_1553147085057_0001_01_000016 taskAttempt attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,603 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Launching attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,604 INFO [ContainerLauncher #4] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:48:28,620 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_3 TaskAttempt Transitioned from FAIL_CONTAINER_CLEANUP to FAIL_TASK_CLEANUP
2019-03-20 22:48:28,621 INFO [CommitterEvent Processor #2] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: TASK_ABORT
2019-03-20 22:48:28,630 WARN [CommitterEvent Processor #2] org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter: Could not delete hdfs://master:9000/user/root/QuasiMonteCarlo_1553147208333_203828452/out/_temporary/1/_temporary/attempt_1553147085057_0001_m_000000_3
2019-03-20 22:48:28,630 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000000_3 TaskAttempt Transitioned from FAIL_TASK_CLEANUP to FAILED
2019-03-20 22:48:28,631 INFO [ContainerLauncher #4] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Shuffle port returned by ContainerManager for attempt_1553147085057_0001_m_000001_3 : 13562
2019-03-20 22:48:28,633 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000000 Task Transitioned from RUNNING to FAILED
2019-03-20 22:48:28,633 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: TaskAttempt: [attempt_1553147085057_0001_m_000001_3] using containerId: [container_1553147085057_0001_01_000016 on NM: [ubuntu3:57320]
2019-03-20 22:48:28,633 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_3 TaskAttempt Transitioned from ASSIGNED to RUNNING
2019-03-20 22:48:28,634 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: Num completed Tasks: 1
2019-03-20 22:48:28,635 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: Job failed as tasks failed. failedMaps:1 failedReduces:0
2019-03-20 22:48:28,636 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: job_1553147085057_0001Job Transitioned from RUNNING to FAIL_WAIT
2019-03-20 22:48:28,637 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_r_000000 Task Transitioned from SCHEDULED to KILL_WAIT
2019-03-20 22:48:28,637 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_3 TaskAttempt Transitioned from RUNNING to KILL_CONTAINER_CLEANUP
2019-03-20 22:48:28,637 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_r_000000_0 TaskAttempt Transitioned from UNASSIGNED to KILLED
2019-03-20 22:48:28,638 INFO [ContainerLauncher #5] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1553147085057_0001_01_000016 taskAttempt attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,638 INFO [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Processing the event EventType: CONTAINER_DEALLOCATE
2019-03-20 22:48:28,638 ERROR [Thread-52] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Could not deallocate container for task attemptId attempt_1553147085057_0001_r_000000_0
2019-03-20 22:48:28,638 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_r_000000 Task Transitioned from KILL_WAIT to KILLED
2019-03-20 22:48:28,638 INFO [ContainerLauncher #5] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,639 INFO [ContainerLauncher #5] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : ubuntu3:57320
2019-03-20 22:48:28,657 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_3 TaskAttempt Transitioned from KILL_CONTAINER_CLEANUP to KILL_TASK_CLEANUP
2019-03-20 22:48:28,657 INFO [CommitterEvent Processor #3] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: TASK_ABORT
2019-03-20 22:48:28,660 WARN [CommitterEvent Processor #3] org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter: Could not delete hdfs://master:9000/user/root/QuasiMonteCarlo_1553147208333_203828452/out/_temporary/1/_temporary/attempt_1553147085057_0001_m_000001_3
2019-03-20 22:48:28,660 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1553147085057_0001_m_000001_3 TaskAttempt Transitioned from KILL_TASK_CLEANUP to KILLED
2019-03-20 22:48:28,660 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1553147085057_0001_m_000001 Task Transitioned from KILL_WAIT to KILLED
2019-03-20 22:48:28,661 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: job_1553147085057_0001Job Transitioned from FAIL_WAIT to FAIL_ABORT
2019-03-20 22:48:28,662 INFO [CommitterEvent Processor #4] org.apache.hadoop.mapreduce.v2.app.commit.CommitterEventHandler: Processing the event EventType: JOB_ABORT
2019-03-20 22:48:29,007 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: job_1553147085057_0001Job Transitioned from FAIL_ABORT to FAILED
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.MRAppMaster: We are finishing cleanly so this is the last retry
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.MRAppMaster: Notify RMCommunicator isAMLastRetry: true
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.rm.RMCommunicator: RMCommunicator notified that shouldUnregistered is: true
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.MRAppMaster: Notify JHEH isAMLastRetry: true
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: JobHistoryEventHandler notified that forceJobCompletion is true
2019-03-20 22:48:29,008 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.MRAppMaster: Calling stop for all the services
2019-03-20 22:48:29,009 INFO [Thread-89] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Stopping JobHistoryEventHandler. Size of the outstanding queue size is 0
2019-03-20 22:48:29,058 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Copying hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job_1553147085057_0001_1.jhist to hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001-1553147212734-root-QuasiMonteCarlo-1553147308635-0-0-FAILED-root.root-1553147220080.jhist_tmp
2019-03-20 22:48:29,096 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Copied to done location: hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001-1553147212734-root-QuasiMonteCarlo-1553147308635-0-0-FAILED-root.root-1553147220080.jhist_tmp
2019-03-20 22:48:29,101 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Copying hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job_1553147085057_0001_1_conf.xml to hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001_conf.xml_tmp
2019-03-20 22:48:29,138 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Copied to done location: hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001_conf.xml_tmp
2019-03-20 22:48:29,195 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Moved tmp to done: hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001.summary_tmp to hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001.summary
2019-03-20 22:48:29,199 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Moved tmp to done: hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001_conf.xml_tmp to hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001_conf.xml
2019-03-20 22:48:29,201 INFO [eventHandlingThread] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Moved tmp to done: hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001-1553147212734-root-QuasiMonteCarlo-1553147308635-0-0-FAILED-root.root-1553147220080.jhist_tmp to hdfs://master:9000/tmp/hadoop-yarn/staging/history/done_intermediate/root/job_1553147085057_0001-1553147212734-root-QuasiMonteCarlo-1553147308635-0-0-FAILED-root.root-1553147220080.jhist
2019-03-20 22:48:29,213 INFO [Thread-89] org.apache.hadoop.mapreduce.jobhistory.JobHistoryEventHandler: Stopped JobHistoryEventHandler. super.stop()
2019-03-20 22:48:29,219 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.rm.RMCommunicator: Setting job diagnostics to Task failed task_1553147085057_0001_m_000000
Job failed as tasks failed. failedMaps:1 failedReduces:0

2019-03-20 22:48:29,219 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.rm.RMCommunicator: History url is http://master:19888/jobhistory/job/job_1553147085057_0001
2019-03-20 22:48:29,278 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.rm.RMCommunicator: Waiting for application to be successfully unregistered.
2019-03-20 22:48:30,281 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Final Stats: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:0 CompletedReds:0 ContAlloc:8 ContRel:0 HostLocal:2 RackLocal:0
2019-03-20 22:48:30,282 INFO [Thread-89] org.apache.hadoop.mapreduce.v2.app.MRAppMaster: Deleting staging directory hdfs://master:9000 /tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001
2019-03-20 22:48:30,286 INFO [Thread-89] org.apache.hadoop.ipc.Server: Stopping server on 56925
2019-03-20 22:48:30,290 INFO [IPC Server listener on 56925] org.apache.hadoop.ipc.Server: Stopping IPC Server listener on 56925
2019-03-20 22:48:30,291 INFO [IPC Server Responder] org.apache.hadoop.ipc.Server: Stopping IPC Server Responder
2019-03-20 22:48:30,292 INFO [TaskHeartbeatHandler PingChecker] org.apache.hadoop.mapreduce.v2.app.TaskHeartbeatHandler: TaskHeartbeatHandler thread interrupted



# worker3： #
**hadoop-root-datanode-ubuntu3.log **

> 2019-03-20 22:44:28,881 INFO org.apache.hadoop.hdfs.server.datanode.VolumeScanner: VolumeScanner(/usr/local/hadoop-2.7.7/hdfs/data, DS-af76597d-bbe1-441c-b2c2-c4a721f1708e): no suitable block pools found to scan.  Waiting 1153551505 ms.
> 2019-03-20 22:44:28,883 ERROR org.apache.hadoop.hdfs.server.datanode.DirectoryScanner: dfs.datanode.directoryscan.throttle.limit.ms.per.sec set to value below 1 ms/sec. Assuming default value of 1000
> 
> ............................................
> 
> 2019-03-20 22:48:35,103 INFO 
>org.apache.hadoop.hdfs.server.datanode.fsdataset.impl.FsDatasetAsyncDiskService: Deleted BP-191184085-127.0.0.1-1552486154804 blk_1073741864_1040 file /usr/local/hadoop-2.7.7/hdfs/data/current/BP-191184085-127.0.0.1-1552486154804/current/finalized/subdir0/subdir0/blk_1073741864
> 2019-03-20 22:48:35,103 INFO org.apache.hadoop.hdfs.server.datanode.fsdataset.impl.FsDatasetAsyncDiskService: Deleted BP-191184085-127.0.0.1-1552486154804 blk_1073741865_1041 file /usr/local/hadoop-2.7.7/hdfs/data/current/BP-191184085-127.0.0.1-1552486154804/current/finalized/subdir0/subdir0/blk_1073741865
> 2019-03-20 23:11:38,287 WARN org.apache.hadoop.hdfs.server.datanode.DataNode: IOException in offerService
> java.io.EOFException: End of File Exception between local host is: "ubuntu3/127.0.0.1"; destination host is: "master":9000; : java.io.EOFException; For more details see:  http://wiki.apache.org/hadoop/EOFException
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
>         at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
>         at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
>         at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
>         at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:765)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1480)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1413)
>         at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:229)
>         at com.sun.proxy.$Proxy15.sendHeartbeat(Unknown Source)
> 




**yarn-root-nodemanager-ubuntu3.log**

> 2019-03-20 22:47:03,553 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.142      OPERATION=Start Container Request       TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000002
> 2019-03-20 22:47:03,553 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from NEW to INITING
> 2019-03-20 22:47:03,554 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Adding container_1553147085057_0001_01_000002 to application application_1553147085057_0001
> 2019-03-20 22:47:03,557 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Application application_1553147085057_0001 transitioned from INITING to RUNNING
> 2019-03-20 22:47:03,561 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000002 transitioned from NEW to LOCALIZING
> 2019-03-20 22:47:03,562 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_INIT for appId application_1553147085057_0001
2019-03-20 22:47:03,563 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event APPLICATION_INIT for appId application_1553147085057_0001
2019-03-20 22:47:03,563 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got APPLICATION_INIT for service mapreduce_shuffle
2019-03-20 22:47:03,565 INFO org.apache.hadoop.mapred.ShuffleHandler: Added token for job_1553147085057_0001
2019-03-20 22:47:03,573 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.jar transitioned from INIT to DOWNLOADING
2019-03-20 22:47:03,573 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.xml transitioned from INIT to DOWNLOADING
2019-03-20 22:47:03,573 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.ResourceLocalizationService: Created localizer for container_1553147085057_0001_01_000002
2019-03-20 22:47:03,683 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.ResourceLocalizationService: Writing credentials to the nmPrivate file /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/nmPrivate/container_1553147085057_0001_01_000002.tokens. Credentials list:
2019-03-20 22:47:03,702 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Initializing user root
2019-03-20 22:47:03,731 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Copying from /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/nmPrivate/container_1553147085057_0001_01_000002.tokens to /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000002.tokens
2019-03-20 22:47:03,732 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Localizer CWD set to /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001 = file:/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001
2019-03-20 22:47:04,988 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.jar(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/10/job.jar) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:47:05,021 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.localizer.LocalizedResource: Resource hdfs://master:9000/tmp/hadoop-yarn/staging/root/.staging/job_1553147085057_0001/job.xml(->/usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/filecache/11/job.xml) transitioned from DOWNLOADING to LOCALIZED
2019-03-20 22:47:05,022 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000002 transitioned from LOCALIZING to LOCALIZED
2019-03-20 22:47:05,052 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000002 transitioned from LOCALIZED to RUNNING
2019-03-20 22:47:05,056 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: launchContainer: [bash, /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000002/default_container_executor.sh]
2019-03-20 22:47:07,668 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Starting resource-monitoring for container_1553147085057_0001_01_000002
2019-03-20 22:47:07,712 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6169 for container-id container_1553147085057_0001_01_000002: 95.6 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:10,746 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6169 for container-id container_1553147085057_0001_01_000002: 94.9 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:13,786 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6169 for container-id container_1553147085057_0001_01_000002: 94.9 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:16,570 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Container container_1553147085057_0001_01_000002 succeeded
2019-03-20 22:47:16,571 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000002 transitioned from RUNNING to EXITED_WITH_SUCCESS
2019-03-20 22:47:16,571 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Cleaning up container container_1553147085057_0001_01_000002
2019-03-20 22:47:16,815 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6169 for container-id container_1553147085057_0001_01_000002: -1B of 1 GB physical memory used; -1B of 2.1 GB virtual memory used
2019-03-20 22:47:16,826 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Deleting absolute path : /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000002
2019-03-20 22:47:16,826 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root OPERATION=Container Finished - Succeeded        TARGET=ContainerImpl    RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000002
2019-03-20 22:47:16,828 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000002 transitioned from EXITED_WITH_SUCCESS to DONE
2019-03-20 22:47:16,828 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Removing container_1553147085057_0001_01_000002 from application application_1553147085057_0001
2019-03-20 22:47:16,829 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_STOP for appId application_1553147085057_0001
2019-03-20 22:47:17,088 INFO SecurityLogger.org.apache.hadoop.ipc.Server: Auth successful for appattempt_1553147085057_0001_000001 (auth:SIMPLE)
2019-03-20 22:47:17,089 INFO SecurityLogger.org.apache.hadoop.ipc.Server: Auth successful for appattempt_1553147085057_0001_000001 (auth:SIMPLE)
2019-03-20 22:47:17,094 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Start request for container_1553147085057_0001_01_000004 by user root
2019-03-20 22:47:17,095 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.142      OPERATION=Start Container Request       TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000004
2019-03-20 22:47:17,095 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Adding container_1553147085057_0001_01_000004 to application application_1553147085057_0001
2019-03-20 22:47:17,096 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000004 transitioned from NEW to LOCALIZING
2019-03-20 22:47:17,096 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_INIT for appId application_1553147085057_0001
2019-03-20 22:47:17,096 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event APPLICATION_INIT for appId application_1553147085057_0001
2019-03-20 22:47:17,096 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got APPLICATION_INIT for service mapreduce_shuffle
2019-03-20 22:47:17,097 INFO org.apache.hadoop.mapred.ShuffleHandler: Added token for job_1553147085057_0001
2019-03-20 22:47:17,098 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000004 transitioned from LOCALIZING to LOCALIZED
2019-03-20 22:47:17,104 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Stopping container with container Id: container_1553147085057_0001_01_000002
2019-03-20 22:47:17,105 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.142      OPERATION=Stop Container Request        TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000002
2019-03-20 22:47:17,127 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000004 transitioned from LOCALIZED to RUNNING
2019-03-20 22:47:17,131 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: launchContainer: [bash, /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000004/default_container_executor.sh]
2019-03-20 22:47:18,839 INFO org.apache.hadoop.yarn.server.nodemanager.NodeStatusUpdaterImpl: Removed completed containers from NM context: [container_1553147085057_0001_01_000002]
2019-03-20 22:47:19,816 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Starting resource-monitoring for container_1553147085057_0001_01_000004
2019-03-20 22:47:19,816 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Stopping resource-monitoring for container_1553147085057_0001_01_000002
2019-03-20 22:47:19,838 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6203 for container-id container_1553147085057_0001_01_000004: 97.9 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:22,870 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6203 for container-id container_1553147085057_0001_01_000004: 96.0 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:25,895 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.monitor.ContainersMonitorImpl: Memory usage of ProcessTree 6203 for container-id container_1553147085057_0001_01_000004: 96.0 MB of 1 GB physical memory used; 1.8 GB of 2.1 GB virtual memory used
2019-03-20 22:47:28,200 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Container container_1553147085057_0001_01_000004 succeeded
2019-03-20 22:47:28,201 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000004 transitioned from RUNNING to EXITED_WITH_SUCCESS
2019-03-20 22:47:28,201 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch: Cleaning up container container_1553147085057_0001_01_000004
2019-03-20 22:47:28,220 INFO org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor: Deleting absolute path : /usr/local/hadoop-2.7.7/hadoop_tmp/nm-local-dir/usercache/root/appcache/application_1553147085057_0001/container_1553147085057_0001_01_000004
2019-03-20 22:47:28,220 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root OPERATION=Container Finished - Succeeded        TARGET=ContainerImpl    RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000004
2019-03-20 22:47:28,221 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000004 transitioned from EXITED_WITH_SUCCESS to DONE
2019-03-20 22:47:28,221 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Removing container_1553147085057_0001_01_000004 from application application_1553147085057_0001
2019-03-20 22:47:28,221 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.AuxServices: Got event CONTAINER_STOP for appId application_1553147085057_0001
2019-03-20 22:47:28,436 INFO SecurityLogger.org.apache.hadoop.ipc.Server: Auth successful for appattempt_1553147085057_0001_000001 (auth:SIMPLE)
2019-03-20 22:47:28,441 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Stopping container with container Id: container_1553147085057_0001_01_000004
2019-03-20 22:47:28,442 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.142      OPERATION=Stop Container Request        TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000004
2019-03-20 22:47:28,444 INFO SecurityLogger.org.apache.hadoop.ipc.Server: Auth successful for appattempt_1553147085057_0001_000001 (auth:SIMPLE)
2019-03-20 22:47:28,460 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.ContainerManagerImpl: Start request for container_1553147085057_0001_01_000006 by user root
2019-03-20 22:47:28,460 INFO org.apache.hadoop.yarn.server.nodemanager.NMAuditLogger: USER=root IP=192.168.213.142      OPERATION=Start Container Request       TARGET=ContainerManageImpl      RESULT=SUCCESS  APPID=application_1553147085057_0001    CONTAINERID=container_1553147085057_0001_01_000006
2019-03-20 22:47:28,463 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.application.ApplicationImpl: Adding container_1553147085057_0001_01_000006 to application application_1553147085057_0001
2019-03-20 22:47:28,463 INFO org.apache.hadoop.yarn.server.nodemanager.containermanager.container.ContainerImpl: Container container_1553147085057_0001_01_000006 transitioned from NEW to LOCALIZING

**userlogs/application_1553147085057_0001/container_1553147085057_0001_01_000002/stderr stdout syslog**

syslog

> 2019-03-20 22:47:16,551 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:56925. Already tried 9 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-03-20 22:47:16,553 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : java.net.ConnectException: Call From ubuntu3/127.0.0.1 to ubuntu3:56925 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
>         at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
>         at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
>         at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
>         at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:732)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1480)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1413)
>         at org.apache.hadoop.ipc.WritableRpcEngine$Invoker.invoke(WritableRpcEngine.java:242)
>         at com.sun.proxy.$Proxy9.getTask(Unknown Source)
>         at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:132)
> Caused by: java.net.ConnectException: Connection refused
>         at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
>         at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
>         at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:206)
>         at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
>         at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
>         at org.apache.hadoop.ipc.Client$Connection.setupConnection(Client.java:615)
>         at org.apache.hadoop.ipc.Client$Connection.setupIOstreams(Client.java:713)
>         at org.apache.hadoop.ipc.Client$Connection.access$2900(Client.java:376)
>         at org.apache.hadoop.ipc.Client.getConnection(Client.java:1529)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1452)
>         ... 4 more
> 
> 2019-03-20 22:47:16,554 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping MapTask metrics system...
> 2019-03-20 22:47:16,554 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system stopped.
> 2019-03-20 22:47:16,554 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system shutdown complete.


## 0419 ##
### secondaryNamenode log ###
2019-04-19 01:47:22,395 ERROR org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode: Exception in doCheckpoint
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Log not rolled. Name node is in safe mode.
The reported blocks 0 needs additional 12 blocks to reach the threshold 0.9990 of total blocks 12.
The number of live datanodes 2 has reached the minimum number 0. Safe mode will be turned off automatically once the thresholds have been reached.
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1335)
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.rollEditLog(FSNamesystem.java:5817)
	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.rollEditLog(NameNodeRpcServer.java:1122)
	at org.apache.hadoop.hdfs.protocolPB.NamenodeProtocolServerSideTranslatorPB.rollEditLog(NamenodeProtocolServerSideTranslatorPB.java:142)
	at org.apache.hadoop.hdfs.protocol.proto.NamenodeProtocolProtos$NamenodeProtocolService$2.callBlockingMethod(NamenodeProtocolProtos.java:12025)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:616)
	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2217)
	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2213)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1762)
	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2211)

	at org.apache.hadoop.ipc.Client.call(Client.java:1476)
	at org.apache.hadoop.ipc.Client.call(Client.java:1413)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:229)
	at com.sun.proxy.$Proxy10.rollEditLog(Unknown Source)
	at org.apache.hadoop.hdfs.protocolPB.NamenodeProtocolTranslatorPB.rollEditLog(NamenodeProtocolTranslatorPB.java:148)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:191)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:102)
	at com.sun.proxy.$Proxy11.rollEditLog(Unknown Source)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doCheckpoint(SecondaryNameNode.java:512)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doWork(SecondaryNameNode.java:395)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode$1.run(SecondaryNameNode.java:361)
	at org.apache.hadoop.security.SecurityUtil.doAsLoginUserOrFatal(SecurityUtil.java:415)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.run(SecondaryNameNode.java:357)
	at java.lang.Thread.run(Thread.java:748)
2019-04-19 01:48:22,611 ERROR org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode: Exception in doCheckpoint
java.io.IOException: Inconsistent checkpoint fields.
LV = -63 namespaceID = 1064787047 cTime = 0 ; clusterId = CID-f90ec84e-62e4-41a0-999f-181946b914d3 ; blockpoolId = BP-191184085-127.0.0.1-1552486154804.
Expecting respectively: -63; 933711425; 0; CID-f491a5e2-a889-43a5-aa4d-7de7be98f613; BP-1469691456-127.0.0.1-1552051967670.
	at org.apache.hadoop.hdfs.server.namenode.CheckpointSignature.validateStorageInfo(CheckpointSignature.java:134)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doCheckpoint(SecondaryNameNode.java:531)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doWork(SecondaryNameNode.java:395)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode$1.run(SecondaryNameNode.java:361)
	at org.apache.hadoop.security.SecurityUtil.doAsLoginUserOrFatal(SecurityUtil.java:415)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.run(SecondaryNameNode.java:357)
	at java.lang.Thread.run(Thread.java:748)
2019-04-19 01:49:22,640 ERROR org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode: Exception in doCheckpoint
java.io.IOException: Inconsistent checkpoint fields.
LV = -63 namespaceID = 1064787047 cTime = 0 ; clusterId = CID-f90ec84e-62e4-41a0-999f-181946b914d3 ; blockpoolId = BP-191184085-127.0.0.1-1552486154804.
Expecting respectively: -63; 933711425; 0; CID-f491a5e2-a889-43a5-aa4d-7de7be98f613; BP-1469691456-127.0.0.1-1552051967670.
	at org.apache.hadoop.hdfs.server.namenode.CheckpointSignature.validateStorageInfo(CheckpointSignature.java:134)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doCheckpoint(SecondaryNameNode.java:531)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.doWork(SecondaryNameNode.java:395)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode$1.run(SecondaryNameNode.java:361)
	at org.apache.hadoop.security.SecurityUtil.doAsLoginUserOrFatal(SecurityUtil.java:415)
	at org.apache.hadoop.hdfs.server.namenode.SecondaryNameNode.run(SecondaryNameNode.java:357)
	at java.lang.Thread.run(Thread.java:748)

