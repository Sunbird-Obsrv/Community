---
description: Definition and details about datasets - a key construct in Obsrv
---

# Datasets

### Introduction

Datasets along with connectors form the core constructs of Obsrv. Anything and everything we do in Obsrv is related to managing a dataset. A dataset can be created with one ore more sources and a dataset can result in creation of one or more tables.

### What does Dataset do?

Most of the time as Engineers, we tend to focus more on technology and current use-cases that we have and the design would be bounded. Hence with data platforms, we try to solve by thinking about the technologies and designs that can enable ingestion, processing, querying and storage and the use-cases at hand that we have. But as a open-source and future proof product - How do we design for evolving needs?

With Obsrv - we took the route of data first and data centric design and at the core of it is a **Dataset**. All the components of obsrv are designed to enable creation, management and consumption of dataset.

With data first thinking - we are able to solve quite a few design problems and helps with explosion of use-cases later:

1. **Data Isolation:** Instead of creating one mega table, datasets enable structuring of data into many datasets further enable data isolation. A dataset can be created per tenant or region. This would help with Data privacy concerns like GDPR where the data has to be stored locally.
2. **Data Governance:** Since a dataset is atomic and can exist indepently, it enables us to govern it more efficiently. Every dataset can have it's own SLA's, Quality metrics, Access Control and derived tables. For ex: Creating a derived table for every tenant can enable one to implement a capability like "Right to be Forgotten" or "Download my data".
3. **Efficient Scaling:** Not all datasets will be of the same size. With the dataset construct - one can theoritically scale a specific dataset, instead of scaling entire Obsrv. Traditional design would scale (or size) for the largest source or peak volume.
4. **Decoupled & Modular:** Each dataset is decoupled with another dataset. One dataset failure doesn't effect another dataset. This enables interesting use-cases like create a dataset on demand from the same source and direct it for adhoc querying without impact production workloads and shutdown the dataset once adhoc analysis is over
5. **Ease of Operations:** At the end of the day, a solution is built once but has to be operated daily. With the dataset construct, even the operations is bifurcated by dataset. This would enable one to focus on critical datasets than all datasets which would result in operational efficiency and reduced operational teams

### Dataset Management

Following lists the high level capabilities available as part of Dataset via dataset management APIs

1. **Create Dataset:** Create dataset by providing or linking sources
2. **Publish Dataset:** Review and Publish a dataset
3. **Manage Dataset:** Perform actions like edit, retire and archive a dataset. Edit of a dataset creates a new version and the changes are propagated to existing dataset on publish
4. **Monitor Dataset:** Monitor dataset operations. Every dataset exposes various metrics like data load, processing speed, queries per second and query throughput
5. **Manage Tables:** Create aggregate tables. Aggregate tables can be created on all or subset of data
6. **Manage Connectors:** Manage source and destination connectors for the dataset
