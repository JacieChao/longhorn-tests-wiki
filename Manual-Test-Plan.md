# Overview

Most of the function tests in Longhorn has been covered by the automation test.

But sometimes it's hard to test certain scenarios in the Automation test, so we have this list of manual testing which should be done before the release.

We're also working on converting the manual tests to the automation test as well. 

# Test cases

The `controller` below is referring to the Longhorn Engine working as the controller. It's not the Kubernetes controller in the Longhorn Manager.

## Physical node down
1. One physical node down should result in the state of that node change to `Down`
2. When using with CSI driver, one node with controller and pod down should result in Kubernetes migrate the pod to another node, and Longhorn volume should be able to be used on that node as well.
3. Reboot the node that the controller attached to. After reboot complete, the volume should be reattached to the node.

## Storage space check
1. *[automatable]* Verify that when a replica got deleted, the storage space would be released from the hard disk.
2. *[automatable]* Verify that when a volume got deleted, the storage space would be released from the hard disk.

## Upgrade test
Old version with both attached volumes and detached volumes. After upgrade:
1. Check the contents of the attached volumes are good.
2. Manager cannot do anything about the attached volumes except detaching it.
3. Manager cannot live-upgrade the attached volumes if the version is incompatible.
4. Manager cannot reattach an existing volume, until the user has upgraded the engine image to a manager supported version.
5. After offline or online (live) engine upgrade, check the contents of the volumes are valid.