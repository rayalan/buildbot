Release Notes for Buildbot |version|
====================================

..
    Any change that adds a feature or fixes a bug should have an entry here.
    Most simply need an additional bulleted list item, but more significant
    changes can be given a subsection of their own.

..
    NOTE: When releasing 0.9.0, combine these notes with those from 0.9.0b{1,2,3,4,5}
    into one single set of notes.  Also, link prominently to the migration guide.

The following are the release notes for Buildbot |version|

See :ref:`Upgrading to Nine` for a guide to upgrading from 0.8.x to 0.9.x

Master
------

Features
~~~~~~~~

* :class:`GitPoller` now has a ``buildPushesWithNoCommits`` option to allow the rebuild of already known commits on new branches.
* Add GitLab authentication plugin for web UI. See :class:`buildbot.www.oauth2.GitLabAuth`.
* :class:`DockerLatentWorker` now has a ``hostconfig`` parameter that can be used to setup host configuration when creating a new container.

Fixes
~~~~~

* Fix loading :class:`~buildbot.ldapuserinfo.LdapUserInfo` plugin and its documentation (:bug:`3371`).
* Fix deprecation warnings seen with docker-py >= 1.4 when passing arguments to ``docker_client.start()``.
* :class:`GitHubEventHandler` now uses the ``['repository']['html_url']`` key in the webhook payload to populate ``repository``, as the previously used ``['url']`` and ``['clone_url']`` keys had a different format between push and pull requests and GitHub and GitHub Enterprise instances.

Deprecations, Removals, and Non-Compatible Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Deprecated ``workdir`` was removed, ``builddir`` property should be used instead.

Changes for Developers
~~~~~~~~~~~~~~~~~~~~~~

Worker
------

Features
~~~~~~~~

Fixes
~~~~~

Deprecations, Removals, and Non-Compatible Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Transition to "worker" terminology
----------------------------------

Since version 0.9.0 of Buildbot "slave"-based terminology is deprecated
in favor of "worker"-based terminology.

For details about public API changes see
:ref:`Transition-to-worker-terminology`.

API changes done without providing fallback:

.. list-table::
   :header-rows: 1

   * - Old name
     - New name

   * - :py:mod:`buildbot.buildslave.manager`
     - :py:mod:`buildbot.worker.manager`

   * - :py:class:`buildbot.buildslave.manager.BuildslaveRegistration`
     - :py:class:`buildbot.worker.manager.WorkerRegistration`

   * - :py:class:`buildbot.buildslave.manager.BuildslaveRegistration.buildslave`
     - :py:class:`buildbot.worker.manager.WorkerRegistration.worker`

   * - :py:class:`buildbot.buildslave.manager.BuildslaveManager`
     - :py:class:`buildbot.worker.manager.WorkerManager`

   * - :py:attr:`buildbot.buildslave.manager.BuildslaveManager.slaves`
     - :py:attr:`buildbot.worker.manager.WorkerManager.workers`

   * - :py:meth:`buildbot.buildslave.manager.BuildslaveManager.getBuildslaveByName`
     - :py:meth:`buildbot.worker.manager.WorkerManager.getWorkerByName`


   * - :py:class:`buildbot.buildslave.docker.DockerLatentBuildSlave`
     - :py:class:`buildbot.worker.docker.DockerLatentWorker`


   * - :py:class:`buildbot.buildslave.local.LocalBuildSlave`
     - :py:class:`buildbot.worker.local.LocalWorker`

   * - :py:attr:`buildbot.buildslave.local.LocalBuildSlave.LocalBuildSlaveFactory`
     - :py:attr:`buildbot.worker.local.LocalWorker.LocalWorkerFactory`

   * - :py:attr:`buildbot.buildslave.local.LocalBuildSlave.remote_slave`
     - :py:attr:`buildbot.worker.local.LocalWorker.remote_worker`


   * - :py:mod:`buildbot.buildslave.base` module with all contents
     - :py:mod:`buildbot.worker.base`


   * - :py:meth:`buildbot.buildslave.AbstractBuildSlave.updateSlave`
     - :py:meth:`buildbot.worker.AbstractWorker.updateWorker`

   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.slavebuilders`
     - :py:attr:`buildbot.worker.AbstractWorker.workerforbuilders`

   * - :py:meth:`buildbot.buildslave.AbstractBuildSlave.updateSlaveStatus`
     - :py:meth:`buildbot.worker.AbstractWorker.updateWorkerStatus`


   * - :py:meth:`buildbot.buildslave.AbstractLatentBuildSlave.updateSlave`
     - :py:meth:`buildbot.worker.AbstractLatentWorker.updateWorker`


   * - :py:class:`buildbot.buildslave.BuildSlave.slave_status`
     - :py:class:`buildbot.worker.Worker.worker_status`


   * - :py:meth:`buildbot.config.MasterConfig.load_slaves`
     - :py:meth:`~buildbot.config.MasterConfig.load_workers`


   * - :py:attr:`buildbot.master.BuildMaster.buildslaves`
     - :py:attr:`buildbot.master.BuildMaster.workers`


   * - :py:attr:`buildbot.process.build.Build.slavebuilder`
     - :py:attr:`~buildbot.process.build.Build.workerforbuilder`

   * - :py:meth:`buildbot.process.build.Build.setSlaveEnvironment`
     - :py:meth:`~buildbot.process.build.Build.setWorkerEnvironment`

   * - :py:attr:`buildbot.process.build.Build.slaveEnvironment`
     - :py:attr:`~buildbot.process.build.Build.workerEnvironment`

   * - :py:meth:`buildbot.process.build.Build.getSlaveCommandVersion`
     - :py:meth:`~buildbot.process.build.Build.getWorkerCommandVersion`

   * - :py:meth:`buildbot.process.build.Build.setupSlaveBuilder`
     - :py:meth:`~buildbot.process.build.Build.setupWorkerForBuilder`

   * - :py:meth:`buildbot.process.builder.Build.canStartWithSlavebuilder`
     - :py:meth:`~buildbot.process.builder.Build.canStartWithWorkerForBuilder`


   * - :py:meth:`buildbot.process.slavebuilder.AbstractSlaveBuilder.getSlaveCommandVersion`
     - :py:meth:`buildbot.process.workerforbuilder.AbstractWorkerForBuilder.getWorkerCommandVersion`

   * - :py:meth:`buildbot.process.slavebuilder.AbstractSlaveBuilder.attached`
       method argument ``slave`` was renamed
     - ``worker``


   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.slave_commands`
     - :py:attr:`buildbot.worker.AbstractWorker.worker_commands`

   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.slave_environ`
     - :py:attr:`buildbot.worker.AbstractWorker.worker_environ`

   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.slave_basedir`
     - :py:attr:`buildbot.worker.AbstractWorker.worker_basedir`

   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.slave_system`
     - :py:attr:`buildbot.worker.AbstractWorker.worker_system`

   * - :py:attr:`buildbot.buildslave.AbstractBuildSlave.buildslaveid`
     - :py:attr:`buildbot.worker.AbstractWorker.workerid`

   * - :py:meth:`buildbot.buildslave.AbstractBuildSlave.addSlaveBuilder`
     - :py:meth:`buildbot.worker.AbstractWorker.addWorkerForBuilder`

   * - :py:meth:`buildbot.buildslave.AbstractBuildSlave.removeSlaveBuilder`
     - :py:meth:`buildbot.worker.AbstractWorker.removeWorkerForBuilder`

   * - :py:meth:`buildbot.buildslave.AbstractBuildSlave.messageReceivedFromSlave`
     - :py:meth:`buildbot.worker.AbstractWorker.messageReceivedFromWorker`


   * - :py:meth:`buildbot.process.slavebuilder.LatentSlaveBuilder`
       constructor positional argument ``slave`` was renamed
     - ``worker``


   * - :py:attr:`buildbot.process.buildrequestdistributor.BasicBuildChooser.nextSlave`
     - :py:attr:`~buildbot.process.buildrequestdistributor.BasicBuildChooser.nextWorker`

   * - :py:attr:`buildbot.process.buildrequestdistributor.BasicBuildChooser.slavepool`
     - :py:attr:`~buildbot.process.buildrequestdistributor.BasicBuildChooser.workerpool`

   * - :py:attr:`buildbot.process.buildrequestdistributor.BasicBuildChooser.preferredSlaves`
     - :py:attr:`~buildbot.process.buildrequestdistributor.BasicBuildChooser.preferredWorkers`

   * - :py:attr:`buildbot.process.buildrequestdistributor.BasicBuildChooser.rejectedSlaves`
     - :py:attr:`~buildbot.process.buildrequestdistributor.BasicBuildChooser.rejectedSlaves`


   * - :py:attr:`buildbot.steps.shell.ShellCommand.slaveEnvironment`
       (Note: this variable is renderable)
     - :py:attr:`buildbot.steps.shell.ShellCommand.workerEnvironment`


   * - :py:mod:`buildbot.status.slave`
     - :py:mod:`buildbot.status.worker`

   * - :py:class:`buildbot.status.slave.SlaveStatus`
     - :py:class:`buildbot.status.worker.WorkerStatus`

   * - :py:meth:`buildbot.interfaces.IStatusReceiver.slaveConnected`
       with all implementations
     - :py:meth:`buildbot.interfaces.IStatusReceiver.workerConnected`

   * - :py:meth:`buildbot.interfaces.IStatusReceiver.slaveDisconnected`
       with all implementations
     - :py:meth:`buildbot.interfaces.IStatusReceiver.workerDisconnected`

   * - :py:meth:`buildbot.status.master.Status.slaveConnected`
     - :py:meth:`buildbot.status.master.Status.workerConnected`

   * - :py:meth:`buildbot.status.master.Status.slaveDisconnected`
     - :py:meth:`buildbot.status.master.Status.workerDisconnected`

   * - :py:meth:`buildbot.status.master.Status.slavePaused`
     - :py:meth:`buildbot.status.master.Status.workerPaused`

   * - :py:meth:`buildbot.status.master.Status.slaveUnpaused`
     - :py:meth:`buildbot.status.master.Status.workerUnpaused`

   * - :py:attr:`buildbot.status.master.Status.buildslaves`
     - :py:attr:`buildbot.status.master.Status.workers`

   * - :py:meth:`buildbot.status.base.StatusReceiverBase.slavePaused`
     - :py:meth:`buildbot.status.base.StatusReceiverBase.workerPaused`

   * - :py:meth:`buildbot.status.base.StatusReceiverBase.slaveUnpaused`
     - :py:meth:`buildbot.status.base.StatusReceiverBase.workerUnpaused`

   * - :py:meth:`buildbot.interfaces.IStatus.getSlaveNames`
       with all implementations
     - :py:meth:`buildbot.interfaces.IStatus.getWorkerNames`

   * - :py:meth:`buildbot.interfaces.IStatus.getSlave`
       with all implementations
     - :py:meth:`buildbot.interfaces.IStatus.getWorker`


   * - :py:meth:`buildbot.interfaces.IBuildStatus.getSlavename`
       with all implementations
     - :py:meth:`buildbot.interfaces.IBuildStatus.getWorkername`

   * - :py:meth:`buildbot.status.build.BuildStatus.setSlavename`
     - :py:meth:`buildbot.status.build.BuildStatus.setWorkername`

   * - :py:attr:`buildbot.status.build.BuildStatus.slavename`
     - :py:attr:`buildbot.status.build.BuildStatus.workername`
       (also it was moved from class static attribute to instance attribute)


   * - :py:meth:`buildbot.interfaces.IBuilderStatus.getSlaves`
       with all implementations
     - :py:meth:`buildbot.interfaces.IBuilderStatus.getWorkers`

   * - :py:attr:`buildbot.status.builder.BuilderStatus.slavenames`
     - :py:attr:`buildbot.status.builder.BuilderStatus.workernames`

   * - :py:meth:`buildbot.status.builder.BuilderStatus.setSlavenames`
     - :py:meth:`buildbot.status.builder.BuilderStatus.setWorkernames`


   * - :py:meth:`buildbot.process.botmaster.BotMaster.slaveLost`
     - :py:meth:`buildbot.process.botmaster.BotMaster.workerLost`

   * - :py:meth:`buildbot.process.botmaster.BotMaster.getBuildersForSlave`
     - :py:meth:`buildbot.process.botmaster.BotMaster.getBuildersForWorker`

   * - :py:meth:`buildbot.process.botmaster.BotMaster.maybeStartBuildsForSlave`
     - :py:meth:`buildbot.process.botmaster.BotMaster.maybeStartBuildsForWorker`


   * - :py:class:`buildbot.locks.RealSlaveLock`
     - :py:class:`buildbot.locks.RealWorkerLock`

   * - :py:attr:`buildbot.locks.RealSlaveLock.maxCountForSlave`
     - :py:attr:`buildbot.locks.RealWorkerLock.maxCountForWorker`


   * - :py:class:`buildbot.protocols.base.Connection`
       constructor positional argument ``buildslave`` was renamed
     - ``worker``

   * - :py:attr:`buildbot.protocols.base.Connection.buidslave`
     - :py:attr:`buildbot.protocols.base.Connection.worker`

   * - :py:meth:`buildbot.protocols.base.Connection.remoteGetSlaveInfo`
     - :py:meth:`buildbot.protocols.base.Connection.remoteGetWorkerInfo`


   * - :py:class:`buildbot.protocols.pb.Connection`
       constructor positional argument ``buildslave`` was renamed
     - ``worker``

Other changes done without providing fallback:

* Functions argument ``buildslaveName`` renamed to ``workerName``.

* Loop variables, local variables, helper functions:

  .. list-table::
     :header-rows: 1

     * - Old name
       - New name

     * - ``s``
       - ``w`` or ``worker``

     * - ``sl``
       - ``w`` or ``worker``

     * - ``bs`` ("buildslave")
       - ``w``

     * - ``sb``
       - ``wfb`` ("worker for builder")

     * - ``bs1()``, ``bs2()``
       - ``w1()``, ``w2()``

     * - ``bslave``
       - ``worker``

     * - ``BS1_NAME``, ``BS1_ID``, ``BS1_INFO``
       - ``W1_NAME``, ``W1_ID``, ``W1_INFO``

* In :py:meth:`buildbot.config.BuilderConfig.getConfigDict` result
  ``'slavenames'`` key changed to ``'workernames'``;
  ``'slavebuilddir'`` key changed to ``'workerbuilddir'``;
  ``'nextSlave'`` key changed to ``'nextWorker'``.

* :py:meth:`buildbot.process.builder.BuilderControl.ping` now generates
  ``["ping", "no worker"]`` event, instead of ``["ping", "no slave"]``.

* ``buildbot.plugins.util.WorkerChoiceParameter``
  (previously ``BuildslaveChoiceParameter``) label was changed from
  ``Build slave`` to ``Worker``.

* ``buildbot.plugins.util.WorkerChoiceParameter``
  (previously ``BuildslaveChoiceParameter``) default name was changed from
  ``slavename`` to ``workername``.

* ``buildbot.status.builder.SlaveStatus`` fallback was removed.
  ``SlaveStatus`` was moved to ``buildbot.status.builder.slave`` previously,
  and now it's :py:class:`buildbot.status.worker.WorkerStatus`.

* :py:mod:`buildbot.status.status_push.StatusPush` events generation changed
  (this module will be completely removed in 0.9.x):

  - instead of ``slaveConnected`` with data ``slave=...`` now generated
    ``workerConnected`` event with data ``worker=...``;

  - instead of ``slaveDisconnected`` with data ``slavename=...`` now generated
    ``workerDisconnected`` with data ``workername=...``;

  - instead of ``slavePaused`` with data ``slavename=...`` now generated
    ``workerPaused`` event with data ``workername=...``;

  - instead of ``slaveUnpaused`` with data ``slavename=...`` now generated
    ``workerUnpaused`` event with data ``workername=...``;

* :py:meth:`buildbot.status.build.BuildStatus.asDict` returns worker name under
  ``'worker'`` key, instead of ``'slave'`` key.

* :py:meth:`buildbot.status.builder.BuilderStatus.asDict` returns worker
  names under ``'workers'`` key, instead of ``'slaves'`` key.

* Definitely privately used "slave"-named variables and attributes were
  renamed, including tests modules, classes and methods.

Database
~~~~~~~~

Database API changes done without providing fallback.

.. list-table::
   :header-rows: 1

   * - Old name
     - New name

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.getBuildslaves`
       (rewritten in nine)
       and
       :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.getBuildslave`
       (introduced in nine)
       results uses instead of ``'slaveinfo'`` key
     - ``'workerinfo'`` key


   * - :py:attr:`buildbot.db.model.Model.buildslaves`
     - :py:attr:`buildbot.db.model.Model.workers`

   * - :py:attr:`buildbot.db.model.Model.configured_buildslaves`
     - :py:attr:`buildbot.db.model.Model.configured_workers`

   * - :py:attr:`buildbot.db.model.Model.connected_buildslaves`
     - :py:attr:`buildbot.db.model.Model.connected_workers`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.findBuildslaveId`
       (introduced in nine)
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.findWorkerId`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.deconfigureAllBuidslavesForMaster`
       (introduced in nine, note typo ``Buidslaves``)
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.deconfigureAllWorkersForMaster`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveConfigured`
       (introduced in nine)
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.workerConfigured`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveConfigured`
       method argument ``buildslaveid`` was renamed
       (introduced in nine)
     - ``workerid``

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.getBuildslave`
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.getWorker`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.getBuildslaves`
       method argument ``_buildslaveid`` was renamed
       (introduced in nine)
     - ``_workerid``

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveConnected`
       (introduced in nine)
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.workerConnected`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveConnected`
       method argument ``slaveinfo`` was renamed
       (introduced in nine)
     - ``workerinfo``

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveConnected`
       method argument ``buildslaveid`` was renamed
       (introduced in nine)
     - ``workerid``

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveDisconnected`
       (introduced in nine)
     - :py:meth:`buildbot.db.workers.WorkersConnectorComponent.workerDisconnected`

   * - :py:meth:`buildbot.db.buildslaves.BuildslavesConnectorComponent.buildslaveDisconnected`
       method argument ``buildslaveid`` was renamed
       (introduced in nine)
     - ``workerid``


   * - :py:meth:`buildbot.db.builds.BuildsConnectorComponent.getBuilds`
       method argument ``buildslaveid`` was renamed
       (introduced in nine)
     - ``workerid``


   * - :py:meth:`buildbot.db.builds.BuildsConnectorComponent.addBuild`
       method argument ``buildslaveid`` was renamed
       (introduced in nine)
     - ``workerid``


   * - :py:class:`buildbot.reporters.message.MessageFormatter`
       template variable ``slavename``
     - ``workername``

Data API
~~~~~~~~

Python API changes:

.. list-table::
   :header-rows: 1

   * - Old name
     - New name

   * - :py:mod:`buildbot.data.buildslaves`
     - :py:mod:`~buildbot.data.workers`

   * - :py:class:`buildbot.data.buildslaves.BuildslaveEndpoint`
     - :py:class:`~buildbot.data.workers.WorkerEndpoint`

   * - :py:class:`buildbot.data.buildslaves.BuildslavesEndpoint`
     - :py:class:`~buildbot.data.workers.WorkersEndpoint`

   * - :py:class:`buildbot.data.buildslaves.Buildslave`
     - :py:class:`~buildbot.data.workers.Worker`

   * - :py:meth:`buildbot.data.buildslaves.Buildslave.buildslaveConfigured`
     - :py:meth:`~buildbot.data.workers.Worker.workerConfigured`

   * - :py:meth:`buildbot.data.buildslaves.Buildslave.findBuildslaveId`
     - :py:meth:`~buildbot.data.workers.Worker.findWorkerId`

   * - :py:meth:`buildbot.data.buildslaves.Buildslave.buildslaveConnected`
     - :py:meth:`~buildbot.data.workers.Worker.workerConnected`

   * - :py:meth:`buildbot.data.buildslaves.Buildslave.buildslaveDisconnected`
     - :py:meth:`~buildbot.data.workers.Worker.workerDisconnected`

   * - :py:meth:`buildbot.data.buildslaves.Buildslave.deconfigureAllBuidslavesForMaster`
     - :py:meth:`~buildbot.data.workers.Worker.deconfigureAllWorkersForMaster`


   * - ``buildslaveid`` in function arguments and API specification
     - ``workerid``

   * - ``slaveinfo`` in function arguments and API specification
     - ``workerinfo``

Changed REST endpoints:

.. list-table::
   :header-rows: 1

   * - Old name
     - New name

   * - ``/buildslaves``
     - ``/workers``

   * - ``/buildslaves/n:buildslaveid``
     - ``/workers/n:workerid``

   * - ``/buildslaves/n:buildslaveid/builds``
     - ``/workers/n:workerid/builds``

   * - ``/buildslaves/:buildslaveid/builds/:buildid``
     - ``/workers/:workerid/builds/:buildid``

   * - ``/masters/n:masterid/buildslaves``
     - ``/masters/n:masterid/workers``

   * - ``/masters/n:masterid/buildslaves/n:buildslaveid``
     - ``/masters/n:masterid/workers/n:workerid``

   * - ``/masters/n:masterid/builders/n:builderid/buildslaves``
     - ``/masters/n:masterid/builders/n:builderid/workers``

   * - ``/masters/n:masterid/builders/n:builderid/buildslaves/n:buildslaveid``
     - ``/masters/n:masterid/builders/n:builderid/workers/n:workerid``

   * - ``/builders/n:builderid/buildslaves``
     - ``/builders/n:builderid/workers``

   * - ``/builders/n:builderid/buildslaves/n:buildslaveid``
     - ``/builders/n:builderid/workers/n:workerid``

Changed REST object keys:

.. list-table::
   :header-rows: 1

   * - Old name
     - New name

   * - ``buildslaveid``
     - ``workerid``

   * - ``slaveinfo``
     - ``workerinfo``

   * - ``buildslave``
     - ``worker``

   * - ``buildslaves``
     - ``workers``

``data_module`` version bumped from ``1.2.0`` to ``2.0.0``.

Web UI
~~~~~~

In base web UI (``www/base``) and Material Design web UI (``www/md_base``)
all "slave"-named messages and identifiers were renamed to use "worker" names
and new REST API endpoints.

MQ layer
~~~~~~~~

``buildslaveid`` key in messages were replaced with ``workerid``.

Details
-------

For a more detailed description of the changes made in this version, see the git log itself:

.. code-block:: bash

   git log v0.9.0b7..master

Older Versions
--------------

Release notes for older versions of Buildbot are available in the :src:`master/docs/relnotes/` directory of the source tree.
Newer versions are also available here:

.. toctree::
    :maxdepth: 1

    0.9.0b7
    0.9.0b6
    0.9.0b5
    0.9.0b4
    0.9.0b3
    0.9.0b2
    0.9.0b1
    0.8.12
    0.8.10
    0.8.9
    0.8.8
    0.8.7
    0.8.6

Note that Buildbot-0.8.11 was never released.
