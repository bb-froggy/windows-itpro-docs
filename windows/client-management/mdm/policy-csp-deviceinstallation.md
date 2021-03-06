---
title: Policy CSP - DeviceInstallation
description: Policy CSP - DeviceInstallation
ms.author: maricia
ms.topic: article
ms.prod: w10
ms.technology: windows
author: MariciaAlforque
ms.date: 12/01/2018
---

# Policy CSP - DeviceInstallation


<hr/>

<!--Policies-->
## DeviceInstallation policies  

<dl>
  <dd>
    <a href="#deviceinstallation-allowinstallationofmatchingdeviceids">DeviceInstallation/AllowInstallationOfMatchingDeviceIDs</a>
  </dd>
  <dd>
    <a href="#deviceinstallation-allowinstallationofmatchingdevicesetupclasses">DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses</a>
  </dd>
  <dd>
    <a href="#deviceinstallation-preventdevicemetadatafromnetwork">DeviceInstallation/PreventDeviceMetadataFromNetwork</a>
  </dd>
  <dd>
    <a href="#deviceinstallation-preventinstallationofdevicesnotdescribedbyotherpolicysettings">DeviceInstallation/PreventInstallationOfDevicesNotDescribedByOtherPolicySettings</a>
  </dd>
  <dd>
    <a href="#deviceinstallation-preventinstallationofmatchingdeviceids">DeviceInstallation/PreventInstallationOfMatchingDeviceIDs</a>
  </dd>
  <dd>
    <a href="#deviceinstallation-preventinstallationofmatchingdevicesetupclasses">DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses</a>
  </dd>
</dl>


<hr/>

<!--Policy-->
<a href="" id="deviceinstallation-allowinstallationofmatchingdeviceids"></a>**DeviceInstallation/AllowInstallationOfMatchingDeviceIDs**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td></td>
	<td></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is allowed to install. 

> [!TIP]
> Use this policy setting only when the "Prevent installation of devices not described by other policy settings" policy setting is enabled. Other policy settings that prevent device installation take precedence over this one.

If you enable this policy setting, Windows is allowed to install or update any device whose Plug and Play hardware ID or compatible ID appears in the list you create, unless another policy setting specifically prevents that installation (for example, the "Prevent installation of devices that match any of these device IDs" policy setting, the "Prevent installation of devices for these device classes" policy setting, or the "Prevent installation of removable devices" policy setting). If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

If you disable or do not configure this policy setting, and no other policy setting describes the device, the "Prevent installation of devices not described by other policy settings" policy setting determines whether the device can be installed.

For more information about hardware IDs and compatible IDs, see [Device Identification Strings](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings).

To get the hardware ID for a device, open Device Manager, right-click the name of the device and click **Properties**. On the **Details** tab, select **Hardware Ids** from the **Property** menu:

![Hardware IDs](images/hardware-ids.png)

<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable.  For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it. For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).


<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Allow installation of devices that match any of these device IDs*
-   GP name: *DeviceInstall_IDs_Allow*
-   GP path: *System/Device Installation/Device Installation Restrictions*
-   GP ADMX file name: *deviceinstallation.admx*

<!--/ADMXBacked-->
<!--SupportedValues-->

<!--/SupportedValues-->
<!--Example-->

<!--/Example-->
<!--Validation-->

<!--/Validation-->
<!--/Policy-->

To enable this policy, use the following SyncML. This example allows Windows to install compatible devices with a device ID of USB\Composite or USB\Class_FF. To configure multiple classes, use `&#xF000;` as a delimiter. 


``` syntax
<SyncML>
    <SyncBody>
        <Replace>
            <CmdID>$CmdID$</CmdID>
            <Item>
                <Target>
                    <LocURI>./Device/Vendor/MSFT/Policy/Config/DeviceInstallation/AllowInstallationOfMatchingDeviceIDs</LocURI>
                </Target>
                <Meta>
                    <Format xmlns="syncml:metinf">string</Format>
                </Meta>
                <Data><enabled/><Data id="DeviceInstall_IDs_Allow_List" value="1&#xF000;USB\Composite&#xF000;2&#xF000;USB\Class_FF"/></Data>
                </Item>
        </Replace>
    </SyncBody>
</SyncML>
```

To verify the policies are applied properly, check C:\windows\INF\setupapi.dev.log and see if the following is listed near the end of the log:

```txt
>>>  [Device Installation Restrictions Policy Check]
>>>  Section start 2018/11/15 12:26:41.659
<<<  Section end 2018/11/15 12:26:41.751
<<<  [Exit status: SUCCESS]
```

<hr/>

<!--Policy-->
<a href="" id="deviceinstallation-allowinstallationofmatchingdevicesetupclasses"></a>**DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td></td>
	<td></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is allowed to install. 

> [!TIP]
> Use this policy setting only when the "Prevent installation of devices not described by other policy settings" policy setting is enabled. Other policy settings that prevent device installation take precedence over this one.

If you enable this policy setting, Windows is allowed to install or update device drivers whose device setup class GUIDs appear in the list you create, unless another policy setting specifically prevents installation (for example, the "Prevent installation of devices that match these device IDs" policy setting, the "Prevent installation of devices for these device classes" policy setting, or the "Prevent installation of removable devices" policy setting). If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

This setting allows device installation based on the serial number of a removable device if that number is in the hardware ID.

If you disable or do not configure this policy setting, and no other policy setting describes the device, the "Prevent installation of devices not described by other policy settings" policy setting determines whether the device can be installed.

For a list of Class and ClassGUID entries for device setup classes, see [System-Defined Device Setup Classes Available to Vendors](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors).

To get the ClassGUID for a device, open Device Manager, right-click the name of the device and click **Properties**. On the **Details** tab, select **Class GUID** from the **Property** menu:

![Class GUIDs](images/class-guids.png)

<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable. For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it. For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).


<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Allow installation of devices using drivers that match these device setup classes*
-   GP name: *DeviceInstall_Classes_Allow*
-   GP path: *System/Device Installation/Device Installation Restrictions*
-   GP ADMX file name: *deviceinstallation.admx*

<!--/ADMXBacked-->
<!--SupportedValues-->

<!--/SupportedValues-->
<!--Example-->

<!--/Example-->
<!--Validation-->

<!--/Validation-->
<!--/Policy-->

To enable this policy, use the following SyncML. This example allows Windows to install:

- Floppy Disks, ClassGUID = {4d36e980-e325-11ce-bfc1-08002be10318}
- CD ROMs, ClassGUID = {4d36e965-e325-11ce-bfc1-08002be10318}
- Modems, ClassGUID = {4d36e96d-e325-11ce-bfc1-08002be10318}

Enclose the class GUID within curly brackets {}. To configure multiple classes, use `&#xF000;` as a delimiter. 


``` syntax
<SyncML>
    <SyncBody>
        <Replace>
            <CmdID>$CmdID$</CmdID>
            <Item>
                <Target>
                    <LocURI>./Device/Vendor/MSFT/Policy/Config/DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses</LocURI>
                </Target>
                <Meta>
                    <Format xmlns="syncml:metinf">string</Format>
                </Meta>
                <Data><enabled/><Data id="DeviceInstall_Classes_Allow_List" value="1&#xF000;{4d36e980-e325-11ce-bfc1-08002be10318}&#xF000;2&#xF000;{4d36e965-e325-11ce-bfc1-08002be10318}&#xF000;3&#xF000;{4d36e96d-e325-11ce-bfc1-08002be10318}"/></Data>
                </Item>
        </Replace>
    </SyncBody>
</SyncML>
```

To verify the policies are applied properly, check C:\windows\INF\setupapi.dev.log and see if the following is listed near the end of the log:


```txt
>>>  [Device Installation Restrictions Policy Check]
>>>  Section start 2018/11/15 12:26:41.659
<<<  Section end 2018/11/15 12:26:41.751
<<<  [Exit status: SUCCESS]
```

<hr/>

<!--Policy-->
<a href="" id="deviceinstallation-preventdevicemetadatafromnetwork"></a>**DeviceInstallation/PreventDeviceMetadataFromNetwork**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td></td>
	<td></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to prevent Windows from retrieving device metadata from the Internet.

If you enable this policy setting, Windows does not retrieve device metadata for installed devices from the Internet. This policy setting overrides the setting in the Device Installation Settings dialog box (Control Panel > System and Security > System > Advanced System Settings > Hardware tab).

If you disable or do not configure this policy setting, the setting in the Device Installation Settings dialog box controls whether Windows retrieves device metadata from the Internet.



<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable.  For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it.  For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).

<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Prevent device metadata retrieval from the Internet*
-   GP name: *DeviceMetadata_PreventDeviceMetadataFromNetwork*
-   GP path: *System/Device Installation*
-   GP ADMX file name: *DeviceSetup.admx*

<!--/ADMXBacked-->
<!--SupportedValues-->

<!--/SupportedValues-->
<!--Example-->

<!--/Example-->
<!--Validation-->

<!--/Validation-->
<!--/Policy-->

<hr/>

<!--Policy-->
<a href="" id="deviceinstallation-preventinstallationofdevicesnotdescribedbyotherpolicysettings"></a>**DeviceInstallation/PreventInstallationOfDevicesNotDescribedByOtherPolicySettings**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td><img src="images/checkmark.png" alt="check mark" /><sup>5</sup></td>
	<td></td>
	<td></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to prevent the installation of devices that are not specifically described by any other policy setting.

If you enable this policy setting, Windows is prevented from installing or updating the device driver for any device that is not described by either the "Allow installation of devices that match any of these device IDs" or the "Allow installation of devices for these device classes" policy setting.

If you disable or do not configure this policy setting, Windows is allowed to install or update the device driver for any device that is not described by the "Prevent installation of devices that match any of these device IDs," "Prevent installation of devices for these device classes," or "Prevent installation of removable devices" policy setting.


<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable.  For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it.  For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).

<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Prevent installation of devices not described by other policy settings*
-   GP name: *DeviceInstall_Unspecified_Deny*
-   GP path: *System/Device Installation/Device Installation Restrictions*
-   GP ADMX file name: *deviceinstallation.admx*

<!--/ADMXBacked-->
<!--SupportedValues-->

<!--/SupportedValues-->
<!--Example-->

<!--/Example-->
<!--Validation-->

<!--/Validation-->
<!--/Policy-->

<hr/>

<!--Policy-->
<a href="" id="deviceinstallation-preventinstallationofmatchingdeviceids"></a>**DeviceInstallation/PreventInstallationOfMatchingDeviceIDs**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device.

If you enable this policy setting, Windows is prevented from installing a device whose hardware ID or compatible ID appears in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

If you disable or do not configure this policy setting, devices can be installed and updated as allowed or prevented by other policy settings.

For more information about hardware IDs and compatible IDs, see [Device Identification Strings](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings).

You can get the hardware ID in Device Manager. For example, USB drives are listed under Disk drives:

![Disk drives](images/device-manager-disk-drives.png)

Right-click the name of the device, click **Properties** > **Details** and select **Hardware Ids** as the **Property**: 

![Hardware IDs](images/disk-drive-hardware-id.png)

<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable.  For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it.  For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).

<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Prevent installation of devices that match any of these device IDs*
-   GP name: *DeviceInstall_IDs_Deny*
-   GP path: *System/Device Installation/Device Installation Restrictions*
-   GP ADMX file name: *deviceinstallation.admx*

<!--/ADMXBacked-->
<!--/Policy-->


<hr/>
To enable this policy, use the following SyncML. This example prevents Windows from installing compatible devices with a device ID of USB\Composite or USB\Class_FF. To configure multiple classes, use `&#xF000;` as a delimiter. To apply the policy to matching device classes that are already installed, set DeviceInstall_IDs_Deny_Retroactive to true. 


``` syntax
<SyncML>
    <SyncBody>
        <Replace>
            <CmdID>$CmdID$</CmdID>
            <Item>
                <Target>
                    <LocURI>./Device/Vendor/MSFT/Policy/Config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs</LocURI>
                </Target>
                <Meta>
                    <Format xmlns="syncml:metinf">string</Format>
                </Meta>
                <Data><enabled/><data id="DeviceInstall_IDs_Deny_Retroactive" value="true"/><Data id="DeviceInstall_IDs_Deny_List" value="1&#xF000;USB\Composite&#xF000;2&#xF000;USB\Class_FF"/></Data>
                </Item>
        </Replace>
    </SyncBody>
</SyncML>
```

To verify the policies are applied properly, check C:\windows\INF\setupapi.dev.log and see if the following is listed near the end of the log:

```txt
>>>  [Device Installation Restrictions Policy Check]
>>>  Section start 2018/11/15 12:26:41.659
<<<  Section end 2018/11/15 12:26:41.751
<<<  [Exit status: SUCCESS]
```

<!--Policy-->
<a href="" id="deviceinstallation-preventinstallationofmatchingdevicesetupclasses"></a>**DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses**  

<!--SupportedSKUs-->
<table>
<tr>
	<th>Home</th>
	<th>Pro</th>
	<th>Business</th>
	<th>Enterprise</th>
	<th>Education</th>
	<th>Mobile</th>
	<th>Mobile Enterprise</th>
</tr>
<tr>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/checkmark.png" alt="check mark" /></td>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
	<td><img src="images/crossmark.png" alt="cross mark" /></td>
</tr>
</table>

<!--/SupportedSKUs-->
<!--Scope-->
[Scope](./policy-configuration-service-provider.md#policy-scope):

> [!div class = "checklist"]
> * Device

<hr/>

<!--/Scope-->
<!--Description-->
This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device.

If you enable this policy setting, Windows is prevented from installing or updating device drivers whose device setup class GUIDs appear in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

If you disable or do not configure this policy setting, Windows can install and update devices as allowed or prevented by other policy settings.

For a list of Class and ClassGUID entries for device setup classes, see [System-Defined Device Setup Classes Available to Vendors](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors).

To get the ClassGUID for a device, open Device Manager, right-click the name of the device and click **Properties**. On the **Details** tab, select **Class GUID** from the **Property** menu:

![Class GUIDs](images/class-guids.png)


<!--/Description-->
> [!TIP]
> This is an ADMX-backed policy and requires a special SyncML format to enable or disable.  For details, see [Understanding ADMX-backed policies](./understanding-admx-backed-policies.md).

> You must specify the data type in the SyncML as &lt;Format&gt;chr&lt;/Format&gt;. For an example SyncML, refer to [Enabling a policy](./understanding-admx-backed-policies.md#enabling-a-policy).

> The payload of the SyncML must be XML-encoded; for this XML encoding, there are a variety of online encoders that you can use. To avoid encoding the payload, you can use CDATA if your MDM supports it.  For more information, see [CDATA Sections](http://www.w3.org/TR/REC-xml/#sec-cdata-sect).

<!--ADMXBacked-->
ADMX Info:  
-   GP English name: *Prevent installation of devices using drivers that match these device setup classes*
-   GP name: *DeviceInstall_Classes_Deny*
-   GP path: *System/Device Installation/Device Installation Restrictions*
-   GP ADMX file name: *deviceinstallation.admx*

<!--/ADMXBacked-->
<!--/Policy-->
<hr/>

To enable this policy, use the following SyncML. This example prevents Windows from installing:

- Floppy Disks, ClassGUID = {4d36e980-e325-11ce-bfc1-08002be10318}
- CD ROMs, ClassGUID = {4d36e965-e325-11ce-bfc1-08002be10318}
- Modems, ClassGUID = {4d36e96d-e325-11ce-bfc1-08002be10318}

Enclose the class GUID within curly brackets {}. To configure multiple classes, use `&#xF000;` as a delimiter. To apply the policy to matching device classes that are already installed, set DeviceInstall_Classes_Deny_Retroactive to true. 


``` syntax
<SyncML>
    <SyncBody>
        <Replace>
            <CmdID>$CmdID$</CmdID>
            <Item>
                <Target>
                    <LocURI>./Device/Vendor/MSFT/Policy/Config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses</LocURI>
                </Target>
                <Meta>
                    <Format xmlns="syncml:metinf">string</Format>
                </Meta>
                <Data><enabled/><data id="DeviceInstall_Classes_Deny_Retroactive" value="true"/><Data id="DeviceInstall_Classes_Deny_List" value="1&#xF000;{4d36e980-e325-11ce-bfc1-08002be10318}&#xF000;2&#xF000;{4d36e965-e325-11ce-bfc1-08002be10318}&#xF000;3&#xF000;{4d36e96d-e325-11ce-bfc1-08002be10318}"/></Data>
                </Item>
        </Replace>
    </SyncBody>
</SyncML>
```

To verify the policies are applied properly, check C:\windows\INF\setupapi.dev.log and see if the following is listed near the end of the log:

```txt
>>>  [Device Installation Restrictions Policy Check]
>>>  Section start 2018/11/15 12:26:41.659
<<<  Section end 2018/11/15 12:26:41.751
<<<  [Exit status: SUCCESS]
```

Footnote:

-   1 - Added in Windows 10, version 1607.
-   2 - Added in Windows 10, version 1703.
-   3 - Added in Windows 10, version 1709.
-   4 - Added in Windows 10, version 1803.
-   5 - Added in Windows 10, version 1809.

<!--/Policies-->

