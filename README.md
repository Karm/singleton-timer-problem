Clustered Singleton Timer problem
=================================
*SOLVED*: [JBoss.org Clustered HA Singleton timer in EAR](https://developer.jboss.org/message/939859#939859)

cluster-ha-singleton
--------------------
* packaged as an ejb
* works steady:

   ```
   [org.jboss.as.quickstarts.cluster.hasingleton.service.ejb.SchedulerBean] (EJB default - 9) HASingletonTimer: Info=HASingleton timer @nodeOne Fri Sep 11 03:03:22 CEST 2015
   ```
ejb-in-ear
----------
* packaged as an ear
* cannot get rid of:

   ```
   ERROR [org.jboss.msc.service.fail] (MSC service thread 1-6) MSC000001: Failed to start service jboss.deployment.subunit."wildfly-ejb-in-ear-ear.ear"."wildfly-ejb-in-ear-ejb.jar".INSTALL: org.jboss.msc.service.StartException in service jboss.deployment.subunit."wildfly-ejb-in-ear-ear.ear"."wildfly-ejb-in-ear-ejb.jar".INSTALL: WFLYSRV0153: Failed to process phase INSTALL of subdeployment "wildfly-ejb-in-ear-ejb.jar" of deployment "wildfly-ejb-in-ear-ear.ear"
    at org.jboss.as.server.deployment.DeploymentUnitPhaseService.start(DeploymentUnitPhaseService.java:163)
    at org.jboss.msc.service.ServiceControllerImpl$StartTask.startService(ServiceControllerImpl.java:1948)
    at org.jboss.msc.service.ServiceControllerImpl$StartTask.run(ServiceControllerImpl.java:1881)
    at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
    at java.lang.Thread.run(Thread.java:745)
   Caused by: java.lang.LinkageError: loader constraint violation: when resolving field "SERVICE_NAME" the class loader (instance of org/jboss/modules/ModuleClassLoader) of the referring class, org/jboss/as/server/ServerEnvironmentService, and the class loader (instance of org/jboss/modules/ModuleClassLoader) for the field's resolved type, org/jboss/msc/service/ServiceName, have different Class objects for that type
    at org.jboss.as.quickstarts.cluster.hasingleton.service.ejb.HATimerServiceActivator.install(HATimerServiceActivator.java:56)
    at org.jboss.as.quickstarts.cluster.hasingleton.service.ejb.HATimerServiceActivator.activate(HATimerServiceActivator.java:44)
    at org.jboss.as.server.deployment.service.ServiceActivatorProcessor.deploy(ServiceActivatorProcessor.java:74)
    at org.jboss.as.server.deployment.DeploymentUnitPhaseService.start(DeploymentUnitPhaseService.java:156)
    ... 5 more
   ```

on service instalaltion. Regardless of playing with the serive names and factory :-(