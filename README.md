# `VMware.CloudFoundation.Reporting`

A PowerShell module for VMware Cloud Foundation reporting.

## Overview

`VMware.CloudFoundation.Reporting` is a PowerShell module that has been written to support the ability to provide insight to the operational state of VMware Cloud Foundation through the use of PowerShell cmdlets. These cmdlets provide quick access to information from the PowerShell console as well as the ability to publish pre-defined HTML reports.

## Requirements

### Platforms

- [VMware Cloud Foundation][vmware-cloud-foundation] 4.2.1 and later

### Operating Systems

- Microsoft Windows Server 2019 and 2022
- Microsoft Windows 10 and 11
- [VMware Photon OS][vmware-photon] 3.0 and 4.0

### PowerShell Editions and Versions

- [Microsoft Windows PowerShell 5.1][microsoft-powershell]
- [PowerShell Core 7.2.0 and later][microsoft-powershell]

### PowerShell Modules

- [`VMware.PowerCLI`][module-vmware-powercli] 12.4.1 and later
- [`VMware.vSphere.SsoAdmin`][module-vmware-vsphere-ssoadmin] 1.3.7 an later
- [`PowerVCF`][module-powervcf] 2.2.0 and later
- [`PowerValidatedSolutions`][module-powervalidatedsolutions] 1.7.0 and later

### Browsers

For the best expereince, use one of the following browsers to view generated HTML reports.

- Microsoft Edge
- Google Chrome
- Mozilla Firefox

## Installing the Module

Verify that your system has a supported edition and version of PowerShell installed.

Install the supporting PowerShell modules from the PowerShell Gallery by running the following commands:

```powershell
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
Install-Module -Name VMware.PowerCLI -MinimumVersion 12.4.1
Install-Module -Name VMware.vSphere.SsoAdmin -MinimumVersion 1.3.7
Install-Module -Name PowerVCF -MinimumVersion 2.2.0
Install-Module -Name PowerValidatedSolutions -MinimumVersion 1.7.0
Install-Module -Name VMware.CloudFoundation.Reporting -RequiredVersion 1.0.0
```

To verify the modules are installed, run the following command in the PowerShell console.

```powershell
Get-InstalledModule
```

Once installed, any cmdlets associated with `VMware.CloudFoundation.Reporting` and the supporting PowerShell modules will be available for use.

To view the cmdlets for available in the module, run the following command in the PowerShell console.

```powershell
Get-Command -Module VMware.CloudFoundation.Reporting
```

To view the help for any cmdlet, run the `Get-Help` command in the PowerShell console.

For example:

```powershell
Get-Help -Name Invoke-VcfHealthReport
```

```powershell
Get-Help -Name Invoke-VcfHealthReport -Examples
```

## User Access

Each cmdlet may provide one or more usage examples. Many of the cmdlets require that credentials are provided to output to the PowerShell console or a report.

The cmdlets in this module, and its dependencies, return data from multple platform components. The credentials for most of the platform components are returned to the cmdlets by retrieving credentials from the SDDC Manager inventory and using these credentials, as needed, within cmdlet operations.

For the best expereince, for cmdlets that connect to SDDC Manager, use the VMware Cloud Foundation API user `admin@local` or an account with the **Cloud Administrator** role in SDDC Manager (e.g., `administratr@vsphere.local`).

## Getting Started with Reports

The PowerShell module provides the ability to generate the following reports:

- [Overview Report](#generating-system-overview-report-tasks)
- [Health Report](#generating-health-report-tasks)
- [Alert Report](#generating-system-alert-report-tasks)
- [Password Policy Report](#generating-password-policy-report-tasks)
- [Configuration Report](#generating-configuration-report-tasks)
- [Upgrade Precheck Report](#generating-upgrade-precheck-report-tasks)

Reports default to a light-mode theme. If you prefer a dark-mode theme, you can use the `-darkMode` parameter with each `Invoke-Vcf*Report` cmdlets. Each report is self-contained and will retain formatting if the resulting HTML output is shared.

Example:

![Screenshot](screenshot.png)

### Generating System Overview Report Tasks

The `Invoke-VcfOverviewReport` cmdlet generates a system overview report. This report contains high-level information about the VMware Cloud Foundation system. This report may be used to provide a quick system overview of the system to your VMware representative.

#### Generate a System Overview Report for a VMware Cloud Foundation Instance

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a system overview report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfOverviewReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath
    ```

    If you prefer to anonymize the data, you can use the `-anonymized` parameter.

    ```powershell
    Invoke-VcfOverviewReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -anonymized
    ```

4. Review the generated HTML report.

### Generating Health Report Tasks

The `Invoke-VcfHealthReport` cmdlet generates a health report. This report combines the SoS Utility health checks with additional health checks not presently available in the SoS Utility for previous VMware Cloud Foundation releases. The report contains detailed information about the health of the VMware Cloud Foundation system and its components.

#### Generate a Health Report for a VMware Cloud Foundation Instance (Display Only Issues)

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a health report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfHealthReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcManagerRootPass $sddcManagerRootPass -reportPath $reportPath -allDomains -failureOnly
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

#### Generate a Health Report for a Workload Domain (Display Only Issues)

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a health report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfHealthReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcManagerRootPass $sddcManagerRootPass -reportPath $reportPath -workloadDomain $workloadDomain -failureOnly
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

### Generate a Health Report for a VMware Cloud Foundation Instance

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a health report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfHealthReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcManagerRootPass $sddcManagerRootPass -reportPath $reportPath -allDomains
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

### Generate a Health Report for a Workload Domain

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a health report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfHealthReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcManagerRootPass $sddcManagerRootPass -reportPath $reportPath -workloadDomain $workloadDomain
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

### Generating System Alert Report Tasks

The `Invoke-VcfSystemAlertReport` cmdlet generates a system alert report. This report collects information about the system alerts that are currently active in the VMware Cloud Foundation system for the platform components. This report reduces the need to login to multiple product interfaces to collect information about the system alerts.

#### Generate a System Alert Report for a VMware Cloud Foundation Instance (Display Only Issues)

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a system alert report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfAlertReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -allDomains -failureOnly
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

#### Generate a System Alert Report for a Workload Domain (Display Only Issues)

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a system alert report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-w01"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-w01"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfAlertReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -workloadDomain $workloadDomain -failureOnly
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

#### Generate a System Alert Report for a VMware Cloud Foundation Instance

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a system alert report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windowa

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfAlertReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -allDomains
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

#### Generate a System Alert Report for a Workload Domain

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a system alert report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windowa

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfAlertReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -workloadDomain $workloadDomain
    ```

4. Review the generated HTML report and perform remediation of any identified issues.

### Generating Password Policy Report Tasks

The `Invoke-VcfPasswordPolicyReport` cmdlet generates a password policy report. This report collects information about the password policy settings in a VMware Cloud Foundation system for the platform components. This report reduces the need to login to multiple product interfaces and endpoints to collect information about the password policy.

#### Generate a Password Policy Report for a VMware Cloud Foundation Instance

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a password policy report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfPasswordPolicy -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -allDomains
    ```

4. Review the generated HTML report.

#### Generate a Password Policy Report for a Workload Domain

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a password policy report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $workloadDomain = "sfo-w01"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $sddcManagerRootPass = "VMw@re1!"
    $workloadDomain = "sfo-w01"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfPasswordPolicy -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -workloadDomain $workloadDomain
    ```

4. Review the generated HTML report.

### Generating Configuration Report Tasks

The `Invoke-VcfConfigurationReport` cmdlet generates a configuration report. This report collects information about the configuration settings in a VMware Cloud Foundation system for the platform components. This report reduces the need to login to multiple product interfaces and endpoints to collect information about the configuration.

#### Generate a Configuration Report for a VMware Cloud Foundation Instance

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a configuration report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfConfigReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -allDomains
    ```

4. Review the generated HTML report.

#### Generate a Configuration Report for a Workload Domain

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate a configuration report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-w01"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-w01"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfConfigReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -workloadDomain $workloadDomain
    ```

4. Review the generated HTML report.

### Generating Upgrade Precheck Report Tasks

The upgrade precheck report, initiates an upgrade precheck of a workload domain using the REST API and presents the results in an HTML report. This allows you to start the precheck from the PowerShell console.

#### Perform an Upgrade Precheck for a Workload Domain

1. Start PowerShell.

2. Replace the values in the sample code with values for the instance of VMware Cloud Foundation to generate an upgrade precheck report for SDDC Manager instance and run the commands in the PowerShell console.

    **Example**: Windows

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-m01"
    $reportPath = "F:\Reporting"
    ```

    **Example**: Linux

    ```powershell
    $sddcManagerFqdn = "sfo-vcf01.sfo.rainpole.io"
    $sddcManagerUser = "admin@local"
    $sddcManagerPass = "VMw@re1!VMw@re1!"

    $workloadDomain = "sfo-m01"
    $reportPath = "/home/vmware/reporting"
    ```

3. Perform the configuration by running the command in the PowerShell console.

    ```powershell
    Invoke-VcfUpgradePrecheck -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -reportPath $reportPath -workloadDomain $workloadDomain
    ```

4. Review the generated HTML report.

# Known Issues

- The `Invoke-VcfPasswordPolicy` cmdlet fails to return collected information for the vCenter Server Password Policy Configuration when using PowerShell Core on Linux

    ```console
    [00-00-0000_00:00:00] INFO Collecting vCenter Server Password Policy Configuration for VMware Cloud Foundation instance (sfo-vcf01.sfo.rainpole.io).

    Connect-SsoAdminServer: One or more errors occurred. (The SSL connection could not be established, see inner exception.)

    Test-SSOAuthentication: Unable to authenticate to Single-Sign-On Server (sfo-w01-vc01.sfo.rainpole.io), check credentials: PRE_VALIDATION_FAILED
    ```

    Workaround: Use PowerShell Core on Windows.

## Support

This module is not supported by VMware Support.

## License

Copyright 2022 VMware, Inc.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

[//]: Links

[microsoft-powershell]: https://docs.microsoft.com/en-us/powershell/
[module-vmware-powercli]: https://www.powershellgallery.com/packages/VMware.PowerCLI/
[module-vmware-vsphere-ssoadmin]: https://www.powershellgallery.com/packages/VMware.vSphere.SsoAdmin
[module-powervcf]: https://www.powershellgallery.com/packages/PowerVCF/2.2.0
[module-powervalidatedsolutions]: https://www.powershellgallery.com/packages/PowerValidatedSolutions
[vmware-photon]: https://vmware.github.io/photon/
[vmware-cloud-foundation]: https://docs.vmware.com/en/VMware-Cloud-Foundation/
