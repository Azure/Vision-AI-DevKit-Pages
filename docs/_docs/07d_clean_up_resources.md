---
title: "Clean up Azure resources"
permalink: /docs/clean_up/
excerpt: "Clean up Azure resources"
variable:
  - platform: windows
    name: Windows
  - platform: macos
    name: macOS
last_modified_at: 2019-04-29
---

## Clean up resources

When going through tutorials and familiarizing yourself with Vision AI Dev Kit and Azure services you may create resources that don't serve a purpose in long term. You can keep the resources and configurations that you created and reuse them, but here are some tips in case you want to delete unnecessary resources.

### Delete Azure resources

Deleting Azure resources and resource groups is irreversible. Make sure that you don't accidentally delete the wrong resource group or resources. If you created the IoT hub inside an existing resource group that has resources that you want to keep, delete only the IoT hub resource itself, instead of deleting the resource group.

To delete the resources:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Resource groups**.

2. Select the name of the resource group that contains your IoT Edge test resources.

3. Review the list of resources contained in your resource group. If you want to delete all of them, you can select **Delete resource group**. If you want to delete only some of them, you can click into each resource to delete them individually.



<!-- ### Delete local resources

If you want to remove the IoT Edge runtime and related resources from your device, use the appropriate commands for your device operating system.

#### Windows

Uninstall the IoT Edge runtime:

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Uninstall-SecurityDaemon
   ```

When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device. View all containers.

   ```powershell
   docker ps -a
   ```

Delete the runtime containers that were created on your device.

   ```powershell
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```

Delete any additional containers that were listed in the `docker ps` output by referring to the container names.

#### Linux

Remove the IoT Edge runtime.

   ```bash
   sudo apt-get remove --purge iotedge
   ```

When the IoT Edge runtime is removed, the containers that it created are stopped, but still exist on your device. View all containers.

   ```bash
   sudo docker ps -a
   ```

Delete the runtime containers that were created on your device.

   ```bash
   docker rm -f edgeHub
   docker rm -f edgeAgent
   ```

Delete any additional containers that were listed in the `docker ps` output by referring to the container names.

Remove the container runtime.

   ```bash
   sudo apt-get remove --purge moby
   ``` -->

