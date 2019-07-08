---
title: Getting Started Guide for Multi-Cloud Backup Storage | UKCloud Ltd
description: Provides information to get up and running with Multi-Cloud Backup Storage
services: mcbs
author: Steve Dixon

toc_rootlink: Getting Started
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Multi-Cloud Backup Storage
toc_fullpath: Getting Started/mcbs-gs.md
toc_mdlink: mcbs-gs.md
---

# Getting Started Guide for Multi-Cloud Backup Storage

## Overview

The UKCloud Multi-Cloud Backup Storage (MCBS) service gives customers a backup target that is accessible from every cloud within UKCloud’s multi-cloud platform, as well as being a remote backup target for customer's on-premises data, utilising a technology that is common across backup products, and compatible with certain file systems, enabling open-source backup applications to utilise the backup service as a target.

UKCloud's Multi-Cloud Backup Storage is based upon Dell EMC's Data Domain Boost (DD Boost) technology, which offers an extensive range of extensions for services such as Oracle, Microsoft SQL, Microsoft Exchange and a wide array of backup server applications to help support performance optimised off-site, multi-cloud backups. A full list of DD Boost extensions can be found in our Multi-Cloud Backup Storage FAQs

### Intended audience

This document is for backup administrators who have:

- Comfortable using an API or command line tools
- Signed-up for UKCloud's Multi-Cloud Backup Storage service
- Been issued their Multi-Cloud Backup Storage credentials

## Multi-Cloud Backup Storage

Multi-Cloud Backup Storage:

- Let’s you pay for what you use, scaling indefinitely and on demand, removing the complexity of capacity management
- Natively enables deduplication, reducing the cost and management of on-premises storage solutions
- Provides easy access to backup storage from any backup application via DDBoost and BoostFS; using Boost protocol vastly simplifies the integration of backup
- applications and Boost-aware databases with a cloud-based backup target by removing the need to rely on file servers or cloud storage gateways
- Can replicate backups to give high levels of data durability and availability, eliminating the need for managing a second backup location

### A full list of DD Boost extensions can be found in our Multi-Cloud Backup Storage FAQs use cases

The low cost of Multi-Cloud Backup Storage per GB, as well as its backup optimised performance and almost unlimited scalability, means there\'s a large variety of use cases for it. For example, it\'s ideal for data archives, backups, databases and log files.

For example:

- Lower overhead of managing backup infrastructure
- Lower Recovery Time Objective (RTO) for backup recovery through more granular or application aware backup applications
- Quicker database recovery, directly from backup target into database
- Greater control over backups using your own self-service backup applications

## Before you begin

When you request your Multi-Cloud Backup Storage service, UKCloud Support creates the following within your account:

- Storage Unit - A storage unit is Multi-Cloud Backup Storage enabled storage pool
- API endpoint (see below)
- API username
- API key (password)

These details form the structure of the personalised credentials you will need to access your Multi-Cloud Backup Storage service

&nbsp;| MCBS API endpoint |
------|-----------------|
**Corsham (Assured)** | |
Internet | TBC - Q2'19 |
PSN Assured | TBC | 
N3 | TBC | 
**Farnborough (Assured)** | |
Internet | `mcbs.frn00013.ukcloud.com` | 
PSN Assured | TBC | 
N3 | TBC | 

Contact UKCloud support if you are unsure which endpoint to use.

### Connecting to Multi-Cloud Backup Storage using Data Domain Boost Filesystem (BoostFS) using Microsoft Windows

For authentication we use local accounts, so the creation of a lockbox is required to store the password and key values for the account. Details on how to create your configuration file, lockbox and mount your storage follows:

#### Configuration file
boostfs.conf contains static configuration that can be used to help connect to your service, key items to configure

`[global]`
`# Data Domain Hostname or IP address`
`data-domain-system=mcbs.frn00013.ukcloud.com` (assumes connection to Farnborough Internet API endpoint)

`# Storage Unit`
`storage-unit={customer storage unit}` (Name of the storage unit as provided in your MCBS credentials)

`# Lockbox path (default: C:\BoostFS\Lockbox\boostfs.lockbox)`
`# lockbox-path=C:\lockbox-name`

`[\\mcbs.frn00013.ukcloud.com\{customer storage unit}]`
`# Drive Letter specifies the Windows drive to map to this UNC mount point`
`drive-letter=G:`

#### Create lockbox
Provide the username and storage unit name for access

`C:\Program Files\BoostFS>boostfs.exe lockbox set -u {username} -d mcbs.frn00013.ukcloud.com -s {customer storage unit} -l C:\BoostFS\LockBox\boostfs.lockbox`

Enter API key (password)

Once created you can use this mount a drive or folder for use with boostfs.

> [!NOTE]
> API key, {username}, {customer storage unit} and API endpoint details will have been provided to you by UKCloud as part MCBS credentials)

#### Mount Storage to local machine
`boostfs.exe mount  \\mcbs.frn00013.ukcloud.com\{customer storage unit}`

This will attempt to mount the volume on the drive G as per the configuration

#### Further Data Domain Boost Filesystem (BoostFS) information

 - For Microsoft Windows, please view the Dell EMC BoostFS for Windows Configuration Guide HERE
 - For Linux, please view the Dell EMC BoostFS for Linux Configuration Guide HERE

## Feedback 

If you have any comments on this document or any other aspect of your UKCloud experience, send them to <products@ukcloud.com>.