---
title: Promotion model types
description: Learn about three common promotion models that are used in cloud migrations. Also, learn how your choice of model affects activities within the migrate and optimize processes.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/22/2021
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: internal
---

# Promotion model types

Workload migration is often discussed as a single activity. In practice, it's a collection of smaller activities that helps the movement of a digital asset to the cloud. One of the last activities in a migration is the promotion of an asset to production. Promotion is the point at which the production system changes for end users. It can often be as simple as changing the network routing, redirecting end users to the new production asset. Promotion is also the point at which IT operations or cloud operations change the focus of operational management processes. The processes change from the previous production system to the new production systems.

There are several promotion models. This article outlines three of the most common ones used in cloud migrations. The choice of a promotion model changes the activities seen within the migrate and optimize processes. As such, promotion model should be decided early in a release.

## Impact of promotion model on migrate and optimize activities

In each of the following promotion models, the chosen migration tool replicates and stages the assets that make up a workload. After staging, each model treats the asset a bit differently.

### Single-step promotion 

In a *single-step* promotion model, the staging process doubles as the promotion process. After all assets are staged, end-user traffic is rerouted and staging becomes production. In such a case, promotion is part of the migration process. This model is the fastest migration model. However, this approach makes it more difficult to integrate robust testing or optimization activities. Further, this model type assumes that the migration team has access to the staging and production environment. This environment compromises separation of duties in some environments.
  > [!NOTE]
  > The table of contents for this site lists the promotion activity as part of the optimize process. In a single-step model, promotion occurs during the migration phase. When using this model, roles and responsibilities should be updated to reflect this.

### Staged 

In a *staged* promotion model, the workload is considered migrated after it's staged, but it isn't yet promoted. Before promotion, the migrated workload undergoes a series of performance tests, business tests, and optimization changes. It's then promoted at a future date with a business test plan. This approach improves the balance between cost and performance, while making it easier to obtain business validation.

### Flight 

The *flight* promotion model combines single-step and staged models. In a flight model, the assets in the workload are treated like production after landing in staging. After a condensed period of automated testing, production traffic is routed to the workload. However, it's a subset of the traffic. That traffic serves as the first flight of production and testing. Assuming the workload works from a feature and performance perspective, more traffic is migrated. After all production traffic has been moved onto the new assets, the workload is considered fully promoted.

The chosen promotion model affects the sequence of activities to be completed. The model also affects the roles and responsibilities of the cloud adoption team. It may even impact the composition of a sprint or multiple sprints.

## Single-step promotion

This model uses migration automation tools to replicate, stage, and promote assets. The assets are replicated into a contained staging environment controlled by the migration tool. After all assets have been replicated, the tool can execute an automated process to promote the assets into the chosen subscription in a single step. While in staging, the tool continues to replicate the asset, minimizing loss of data between the two environments. After an asset is promoted, the linkage between the source system and the replicated system is severed. In this approach, if other changes occur in the initial source systems, the changes are lost.

### Pros 

Positive benefits of this approach include:

- This model introduces less change to the target systems.
- Continuous replication minimizes data loss.
- If a staging process fails, it can quickly be deleted and repeated.
- Replication and repeated staging tests enable an incremental scripting and testing process.

### Cons 

Negative aspects of this approach include:

- Assets staged within the tools-isolated sandbox don't allow for complex testing models.
- During replication, the migration tool consumes bandwidth in the local datacenter. Staging a large volume of assets over an extended duration has an exponential impact on available bandwidth, hurting the migration process and potentially affecting performance of production workloads in the on-premises environment.

## Staged promotion

The staging sandbox managed by the migration tool in this model is used for limited testing purposes. The replicated assets are then deployed into the cloud environment, which serves as an extended staging environment. The migrated assets run in the cloud, while extra assets are replicated, staged, and migrated. When full workloads become available, richer testing is started. When all assets associated with a subscription have been migrated, the subscription and all hosted workloads are promoted to production. There's no change to the workloads in this scenario during the promotion process. Instead, the changes tend to be at the network and identity layers, routing users to the new environment and revoking access of the cloud adoption team.

### Pros

Positive benefits of this approach include:

- This model provides more precise business testing opportunities.
- The workload can be studied more closely to better optimize performance and cost of the assets.
- A larger number of assets can be replicated within similar time and bandwidth constraints.

### Cons 

Negative aspects of this approach include:

- The chosen migration tool can't assist ongoing replication after migration.
- A secondary means of data replication is required to synchronize data platforms during the staged time frame.

## Flight promotion

This model is similar to the staged promotion model. There's one fundamental difference, though. When the subscription is ready for promotion, end-user routing happens in stages or flights. At each flight, extra users are rerouted to the production systems.

### Pros 

Positive benefits of this approach include:

- This model mitigates the risks associated with a large migration or promotion activity. Errors in the migrated solution can be identified with less impact to business processes.
- It allows for monitoring of workload performance demands in the cloud environment for an extended duration, increasing asset-sizing decision accuracy.
- Larger numbers of assets can be replicated within similar time and bandwidth constraints.

### Cons

Negative aspects of this approach include:

- The chosen migration tool can't assist ongoing replication after migration.
- A secondary means of data replication is required to synchronize data platforms during the staged time frame.

## Next steps

After a promotion model is defined and accepted by the cloud adoption team, [remediation of assets](./remediate.md) can begin.

> [!div class="nextstepaction"]
> [Remediating assets prior to migration](./remediate.md)
