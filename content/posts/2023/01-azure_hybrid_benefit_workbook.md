---
title: "Tracking Azure Hybrid Benefit with Workbooks"
date: 2023-04-18T10:17:11-04:00
draft: false
type: post
url: /azure_hybrid_benefit_workbook/
categories:
  - Azure
  - Linux
  - Windows
tags:
  - Windows Virtual Machines
  - Linux Virtual Machines
  - Azure Hybrid Use Benefit
---

## What is Azure Hybrid Benefit?
[Azure Hybrid Benefit](https://azure.microsoft.com/en-gb/pricing/hybrid-benefit/) is a licensing program that allows you to bring your on-premises core-based Windows Server, SQL Server, and Red Hat Linux licenses with active Software Assurance (or subscription) to Azure. Utilizing this benefit can save considerable cost by eliminating the hourly licensing charges for Azure resources, allowing you to pay only for hardware resources. By leveraging Azure Hybrid Benefit, you can optimize your cloud infrastructure costs.

## Keeping track of Azure Hybrid Benefit Usage
Managing and keeping track of Azure Hybrid Benefit entitlements can be challenging however, especially for organizations with a large number of licenses and virtual machines. Ensuring that you are utilizing your entitlements effectively while maintaining compliance with licensing agreements requires careful monitoring and management. It is essential to have a clear understanding of your organization's licensing landscape and to establish processes for tracking and applying Azure Hybrid Benefit entitlements.

I've created this Workbook to simplify the management of Azure Hybrid Benefit in your environment. [Azure Workbooks](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-overview) provide a flexible, interactive, and customizable way to visualize and analyze your Azure resources. By querying the [Azure Resource Graph](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview), the report gathers real-time information about your virtual machines' usage of Azure Hybrid Benefit and creates visualizations to help you understand your licensing landscape.

![AHB](/images/ahb_dashboard_example.png)

## Getting started
You can deploy the workbook to your environment by clicking the blue button:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frlowellfl%2Fazure_workbooks%2Fmain%2Fhybrid_benefit_tracker_workbook.json)

Select your preferred Subscription, Resource Group, and Region to store the dashboard resource. Leave all other fields as-is.
Once the resource is created, open the Dashboard.
Fill in the AHB Entitlement field in the upper left corner with the number of Azure Hybrid Benefit cores which your organization is entitled to.
The workbook will then use the Azure Resource Graph to query all Windows Server virtual machines and display your total virtual machine cores, AHB cores utilized, and AHB cores available.
The workbook will also analyze whether a virtual machine is an optimal use of Azure Hybrid Benefit, as machines with less than 8 vCPUs still consume a minimum of 8 Azure Hybrid Benefit cores.
Please note the following important points when using this tool:

* This dashboard currently only provides information on Windows Server utilization. SQL Server on Azure VMs, SQL Managed Instance, Azure SQL, and Red Hat Linux are not included in this report. Keep an eye on the [repository](https://github.com/rlowellfl/azure_hybrid_benefit_workbook) for future updates and additional views.
* The charts and resources below are based on the Virtual Machines which your user account has RBAC access to view. Virtual machines in other tenants, management groups, subscriptions, or resource groups which are not visible to you will not be calculated and the totals above may be inaccurate. Please ensure that your organization [remains in compliance](https://learn.microsoft.com/en-us/windows-server/get-started/azure-hybrid-benefit?source=recommendations#how-to-maintain-compliance) with all license terms and conditions for Azure Hybrid Benefit.