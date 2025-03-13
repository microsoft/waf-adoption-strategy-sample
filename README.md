# Adoption Strategy for Well Architected Framework (WAF) Reliability (Sample)

Sample Adoption Strategy for Well Architected Framework (WAF) Reliability. Many defintions require further development like for example definition of roles and responsibilities and it is highly dependant on actual organizational structure.

## Metadata

- Version: 0.5

## Content

- [Document Audience](#document-audience)
- [Introduction](#introduction)
- [Scope](#scope)
- [Strategy Objectives and KPIs](#strategy-objectives-and-kpis)
- [Key Strategy Principles](#key-strategy-principles)
- [Current (WAF Adoption) State](#current-waf-adoption-state)
- [WAF Adoption Solution Options (Target State)](#waf-adoption-solution-options-target-state)
- [Roles and Responsibilities](#roles-and-responsibilities)
- [Strategy and Delivery Dependencies](#strategy-and-delivery-dependencies)
- [Adoption (Transition) Plan (Strategic Initiatives)](#adoption-transition-plan-strategic-initiatives)
- [Governance](#governance)
- [Communication Plan](#communication-plan)
- [Risk Management]()


## Document Audience


| Audience                               | Role                                                                                           |
| -------------------------------------- | ---------------------------------------------------------------------------------------------- |
| WAF Adoption Strategy development team | The document captures key concepts and decisions as result of interactive v-team collaboration |
| Department Cloud Technology Leader(s)  | Documented strategy to be reviewed and approved by                                             |


## Introduction

The [Azure Well-Architected Framework (WAF)](https://learn.microsoft.com/azure/well-architected/) is a design framework that can improve the quality of a workload by helping it to:
- Be resilient, available, and recoverable.
- Be as secure as you need it to be.
- Deliver a sufficient return on investment.
- Support responsible development and operations.
- Accomplish its purpose within acceptable timeframes.
  
The framework is founded on the five pillars of architectural excellence, which are mapped to those goals. They are: [Reliability](https://learn.microsoft.com/azure/well-architected/reliability/), Security, Cost Optimization, Operational Excellence, and Performance Efficiency.

The WAF Adoption Strategy outlines the approach for adopting the WAF within an department or Business Unit. The purpose of this strategy is to ensure that our cloud solutions are designed, implemented, and operated in a manner that aligns with best practices for reliability, security, cost optimization, operational excellence, and performance efficiency.
This document serves as a guide for the WAF Adoption Strategy team and Department Cloud Technology Leaders, providing a structured approach to integrating WAF principles into our cloud solution design and operations. By following this strategy, we aim to improve the overall quality of our Azure services without compromising on delivery speed and agility.
The strategy includes detailed plans for leveraging Azure Advisor, Azure Policy Compliance, and other tools to achieve our objectives. It also outlines key adoption principles, roles and responsibilities, and a phased transition plan to ensure a smooth and effective implementation.
By adopting the Azure Well Architected Framework, we aim to enhance our cloud infrastructure's resilience, security, and efficiency, ultimately delivering better value to our stakeholders.

## Scope

- WAF - Reliability, initial scope with intent to expand to other WAF pillars in later adoption phases 
- Azure Cloud usage within a department / business unit, with aim to propose reuse of the department efforts within other BUs or on the Global level.
- Azure Infrastructure and Platform services, the Azure WAF framework is applicable to Application design a well, but it is not current focus of the adoption strategy.


## Strategy Objectives and KPIs

### Parent Organizational or Department Objectives

TBD

### Objective 1

Improve Azure infrastructure and platform service related quality

- Key Results
  - MTBF is reduced by 10% by end of Q4 2025
  - Measured Availability vs. Availability SLOs is improved by 10% by end of Q4 2025

Please also see [Strategy and Delivery Dependencies](#strategy-and-delivery-dependencies)

### Objective 2

Improving the quality does not negatively impact delivery velocity

- Key Results
  -  Code commit to production duration is not increased for more than 10% as result of meeting Objective 1 (by end of Q4 2025)
  -  Number of releases is not decreased for more than 10% as result of meeting Objective 1 (by end of Q4 2025)

## Key Strategy Principles

1. **Reuse (external or internal)** - instead of developing be spoke solutions and frameworks
2. **Automate when possible** - Prefer automation (codifying the process) over writing guidance documents with directions how to implement the WAF best practices
3. **Deliver in increments** - Leverage Lean/Agile concepts and deliver WAF adoption solutions in small increments (e.g. 2-3 weeks), with each increment providing the value
4. **Advise instead of enforce** - Purpose of this strategy is develop advised solution to help teams achieve their quality metrics (1) rather than enforce proposed WAF Adoption solutions in any way.

(1) Teams/Applications should be measured by software delivery Quality and Delivery Velocity metrics. Definition of such metrics is out of scope of this strategy.

## Current (WAF Adoption) State

Application and Infrastructure teams are available of Azure WAF but there is no structured approach for the consistent and measurable adoption.
Some sporadic Microsoft (WARA) - Well Architected Framework Reliability Assessments were delivered in the organization. 

## WAF Adoption Solution Options (Target State)

Following are the proposed solutions and tools to be leveraged for the WAF Adoption:

| Solution                                                                        | % of WAF practices coverage                                                                              |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Azure Advisor                                                                   | approx 30%                                                                                               |
| [Azure Policy](#azure-policy-)                                                  | potential to reach approx. 70% (with custom Policies included)                                           |
| [Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/) | approx 30% (currently), target will be approx 70% - not all recommendations from the WAF can be codified |
| Microsoft WAF Reliability Assessment (WARA)                                     | approx 99%                                                                                               |
| Documented Standards and Guidelines                                             | to cover any remaining gaps not covered by automation                                                    |
| DevOps (CI/CD) pipelines                                                        | to cover any remaining gaps not covered by automation                                                    |


### Application quality Classification and level of WAF recommendation compliance

Different applications require varying levels of quality. The Microsoft WAF frameworks recommend classifying applications and mapping best practices to each application class. Not all recommendations are applicable to every application class.
For example, application classes could include: Mission Critical, Business Critical, and Supporting. A Mission Critical application might require all recommendations to be applied, while a Supporting application may only need a smaller subset.
Therefore, it is important to apply WAF adoption solutions with application classification in mind to avoid creating unrealistic quality expectations for less critical applications.

Please see following articles for more detailed information about Application quality or criticality classification:
- [Azure Well Architected Framework - Assign a criticality rating to each flow](https://learn.microsoft.com/azure/well-architected/reliability/identify-flows#assign-a-criticality-rating-to-each-flow)
- [Azure Cloud Adoption Framework - Criticality scale](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/considerations/criticality#criticality-scale)

### Solution Options

#### 1) Azure Advisor

Azure Advisor for reliability is a feature within Azure Advisor that provides recommendations to help you improve the reliability of your Azure resources.
Reliability in this context refers to the ability of a system to recover from failures and continue to function.
Azure Advisor analyzes your resource configurations and usage telemetry and then provides best practices and recommendations to enhance the reliability of your applications and services.

> [!NOTE]
> Application quality class consideration - Advisor recommendation would need to be mapped in some way to the application quality class. Detailed solution design is out of scope of this strategy document.


##### Assumptions and Constraints
- Only subset of WAF recommendations is covered with current Azure Advisor (Portal) capability (i.e. 30%?), therefore Advisor alone would not be sufficient to provide high level of WAF best practices coverage.
- Certain WAF recommendations will never be available within the Azure Advisor given that some of these recommendations are design and process recommendation, therefore not suitable for tool based assessment of deployed Azure resources.

##### Solution 

- Azure Advisor should be integrated in CI/CD pipeline
  - Ideally, to be implemented as a quality gate for the application which fails in case Advisor % of recommendations are not met
  - Quality gate approval should be implemented (accept or reject the Advisor gate)
  - Application should not be deployed to production without achieving expected percentage of compliance

This quality gate could be implemented as a Task in the pipeline or as a manual validation expected from the team.

![alt text](./assets/image.png)

#### 2) Azure Policy

Azure Policy is a service in Azure that enables you to create, assign, and manage policies to enforce organizational standards and assess compliance at scale.
These policies help ensure that your resources are compliant with your corporate standards and service level agreements (SLAs).

There is number of our of box polices aimed to check reliability related configuration of Azure Services. Custom Policies can be also written with the same goal.
It would be recommended to close WAF best practices gaps not covered by Azure Advisor by deploying our of box Azure Policies covering WAF Reliability best practices and to consider writing custom Policies in case other defined WAF adoption Solutions are not adequate.


> [!NOTE]
> Application quality class consideration - Advisor recommendation would need to be mapped in some way to the application quality class. Detailed solution design is out of scope of this strategy document.

##### Solution 

- WAF related policies are using Audit effect (not preventing deployment of resources)
- Deployed Azure resources are evaluated by the Policy and Policy compliance report is generated
- CI/CD pipeline uses Policy compliance (e.g. over subscription if subscription is scoped to the Application) as a quality check and gate
- One of the approaches for mapping the Application Class with a WAF Quality Class and associated Policies is use of Azure Management Groups or Tags to group/tag Application resources to a corresponding class.
  - Example: Mission Critical app is deployed to "Mission Critical" Management Group which has "WAF Mission Critical" Policy Initiative assigned. 

#### 3) Azure Verified Modules (AVM)

Azure Verified Modules (AVM) are pre-built, reusable infrastructure as code (IaC) modules that have been verified by Microsoft to meet best practices for security, reliability, and operational excellence.
These modules are designed to simplify the deployment and management of Azure resources by providing standardized, tested, and validated templates that can be easily integrated into your infrastructure.

##### Solution 

- Use AVMs to deploy Azure Resources and apply adequate WAF Reliability configuration
- Organization or Department specific WAF configuration may be required to implement [Quality Classification Mapping](#application-quality-classification-and-level-of-waf-recommendation-compliance) 

#### 4) Documented Guidance and Standard

Document any WAF best practices not covered by other "automated" solutions as a Guidance or Internal Standard.

#### 5) Microsoft WAF Reliability Assessment (WARA)

The Microsoft Well Architected Framework (WAF) Reliability Assessment (WARA) is a structured engagement provided by Microsoft as a professional service, designed to help organizations evaluate and improve the reliability of their Azure cloud solutions.
It involves a detailed assessment of the current state of the organization's cloud infrastructure, identifying gaps and areas for improvement based on WAF best practices.
The VBD typically includes interactive sessions with key stakeholders to discuss findings, prioritize recommendations, and develop a roadmap for implementing reliability enhancements.
The goal is to ensure that the organization's cloud solutions are resilient, reliable, and aligned with industry standards.

It would be recommended that WARA is conducted occasionally on few selected applications as a third-party conducted quality check. The WARA is not meant to be conducted for every application in the application portfolio. 

#### 6) DevOps CI/CD Pipeline

CI/CD Pipeline's role would be to codify the process and act as an overall orchestrator of the multiple WAF adoption solutions. WAF may be simply a manual quality gate (check) in the pipeline.
Alternative could be use of Agile definition of done or pull request rules to define expected level of WAF compliance during the commit or completion of User Story.

### Solution to lifecycle (SDLC/ALM) mapping


| Solution                                    | Design | Dev/Test | Production/Operations |
| ------------------------------------------- | ------ | -------- | --------------------- |
| Azure Advisor                               | x      | x        |                       |
| Azure Policy                                |        | x        |                       |
| Azure Verified Modules                      | x      | x        |                       |
| Microsoft WAF Reliability Assessment (WARA) |        |          | x                     |
| Documented Standards                        | x      |          |                       |
| DevOps CI/CD Pipelines (2)                  |        | x        | x                     |

(2) CI/CD Pipeline's role would be to codify the process and act as an overall orchestrator of the multiple WAF adoption solutions. WAF may be simply a manual quality gate (check) in the pipeline.


## Roles and Responsibilities

Proposed model for design and delivery of WAF Adoption strategy is "Inner-sourcing" model with Centralized ownership and federated contribution by multiple departments (Business Units).

### Role Descriptions

- Department - Cloud Solution Architect
- Department - Head of CCoE
- Department - App technical lead
- Central IT - Cloud (Azure) Quality Enabling Service Owner
- Central IT - Head of Cloud Transformation 


| Responsibility                               | Department Cloud Solution Architect | Department Head of CCoE | Department App technical lead |
| -------------------------------------------- | ----------------------------------- | ----------------------- | ----------------------------- |
| Develop the WAF Adoption strategy            | R                                   | A                       | C                             |
| Develop WAF Adoption solutions               | R(?)                                | A                       | C                             |
| Ensure compliance with WAF Adoption strategy | A                                   | A                       | R                             |


## Strategy and Delivery Dependencies

### Other Strategies and Frameworks

- System (Quality) Classification Framework; Organization or department system classification definitions (framework) which can be used to map level of WAF best practices required per each class/category (1). 
- System and Software delivery (quality and velocity) metrics; Organization global or department (BU) level definition of system and software delivery performance metrics (1).

(1) If such definition/framework doesn't exist, it would be recommended to define it (it is out of scope for this Strategy)

### Strategy Execution Dependencies

- Other project dependencies; Any projects which are directly impacted by the strategy (or the lack of the strategy). Example, pending project where there is expectation that Azure WAF is applied but there is no clear definition / guidance how it will be applied.
- Other similar efforts across organization; Possible other departments or global organization functions (e.g. Global Architecture, Global Cloud Platform) who are working or considering owning such strategy and adoption framework


## Adoption (Transition) Plan (Strategic Initiatives)

Recommendation is to define WAF Adoption as a product/service with its own Goals, owner, scope, lifecycle and delivery. Delivery could be broken into following Releases:
- Release 1: Azure Advisor
- Release 2: Azure Policies
- Release 3: Azure Verified Modules
- Release 4: Documented Guidelines and Standards

Release could follow standard department's Release cycle (duration), otherwise, recommendation is for the Release to have two months long cycle (release every two months).

Microsoft WAF Reliability Assessment (WARA) can be delivered by Microsoft at any point. What may be required is definition of the internal WARA usage process (e.g. how to analyze WARA reports, how and when to adopt the finding, etc)

## Governance

[Framework for overseeing the implementation and ongoing management of the strategy.]

## Communication Plan

[How the strategy will be communicated to stakeholders.]

## Risk Management

## Further Improvements

- Propose and agree Group's ownership of the WAF Adoption strategy framework

## References

- [Azure Well-Architected Framework](https://learn.microsoft.com/azure/well-architected/)

