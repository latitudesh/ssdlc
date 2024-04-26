## Requirements Definition

Projects are defined and prioritized based on an internal data-driven standard. Each project has its own set of requirements and related documents (PRDs). Several projects have related internal documents that are reviewed periodically. Document authors can set an expiry date for each document and get an alert when it's due for review.

PRD documents are comprised of:

- Problem statement;
- Objective;
- Key outcomes;
- Work items;
- Security;
- Reference links;

Internal documents derived from PRDs are throughly reviewed every time the underlying premises change. This drives the team to have a clear understanding of required solutions on future projects and the important aspects we need to pay attention to.

Internal documents are usually reviewed every six months. For projects that are constantly updated, it depends on how often the project is changing. The period can vary from one to six months.

### Problem Statement

The description of the problem and its impact on the business, how it  helps users, and how it aligns with Latitude.sh’s business objectives. If a problem comes from internal feedback, feedback authors are asked to contribute both the PRD and the internal documents derived from it.

### Objective

A single sentence describing what the document strives to achieve. It must be clear and short.

### Key Outcomes

Keys outcomes are our definition of success for each project. It's what we expect to achieve when the work items are done. This guarantees that everyone involved works only on the mentioned parts and not spend time thinking or working on a step not mentioned in the document. Some requirements can be misunderstood and people can work on topics that are not expected.

It is especially useful for MVPs as it has multiple iterations.

### Work Items

The description of the items to accomplish that goal. Here we introduce the technical bits and how to go about them. It must be descriptive and linked to the security section.

### Security

A list of descriptive evaluated risks by the team are strictly referenced in PRDs. It must cover topics related to access control, stored data, possible threats, sensitive data (which must be discussed by multiple stakeholders and reviewed during the development process), and topics useful for penetration testing.

It is worth mentioning that every risk must be considered when completing the respective project. If it is a security risk, it must be covered while our team is working on it or addressed before it goes to production. All security items are linked to the respective work items.
<br/><br/>

## Design

The design phase is when we start thinking about how the things will be connected and deliver value to users. It includes dynamic steps based on the type of project.

Therefore, developers and stakeholders can better visualize the big picture and how to accomplish the requirements. This step is usually broken down in multiple iterations.

The design includes exploratory tests to validate tools, identify which dependencies are needed, and describe the proposed solution in detail. This section also covers how we store data and who has access to what resources.

### Threat Modeling

This step represents a table on each project containing all the possible aspects raised by the team that could affect our systems or data. It is important to mention that this is recent in [Latitude.sh](http://Latitude.sh), so we don’t have a list of threat modeling for past projects, but we’ve been doing it since April 2024.

It covers everything about how the systems share data with each other, who can access a specific resource, how the data could be leaked, and possible threats that could affect fragile parts of the project.

Here, the Platform and Product teams work together to create disaster scenarios and evaluate what could affect us by applying different perspectives to validate the possible threats.

### Security Review

Security Review is linked to Work Items, where we define which errors the flow could have and what we think could fail. We define the scope of the project on the Key Outcomes; the Security review uses the definition to validate what must be addressed before release to production and document all the possibilities that [Latitude.sh](http://Latitude.sh) could be exposed to.

New dependencies and tools are included in this section as they could be potentially dangerous and this review is important for the whole project.
<br/><br/>

## Development

To guarantee the effectiveness of our development process, we have defined standards for the team regarding access, security, and workflow.

### Access Control

Each collaborator belongs to a team with access to the internal systems and projects based on this role, the accesses are managed by SAML and the manager can edit or revoke access quickly. If sensitive data leaks to anyone that is not or ceases to be a steakholder, that data is reviewed. E.g., API tokens are rolled every few months and every time an employee leaves or changes roles within the company. 

### Logging and Monitoring

We log everything that's relevant, even when some logs are not actionable. We validate whether they are valid and can provide important information about a specific context. Logs are defined as info, error, or warning. No sensitive data is logged on our services.

We adopt multiple tools to validate the logs:

- Bugsnag: application-level errors that happened to the user
- Datadog: health metrics and internal dashboards
- Axiom: raw logs from our services

### Dependencies Check

Dependable is a GitHub bot that continuously monitors for updated and potential vulnerabilities for dependencies. We review every single alert and apply the necessary measures. We focus on working with the most recent dependencies’ version possible, so we double-check our dependencies every month and evaluate what we can upgrade.

### Development Workflow

[Latitude.sh](http://Latitude.sh) follows a standard workflow similar to Basecamp's **[Six-Week Cycle](https://3.basecamp-help.com/article/35-the-six-week-cycle).** For six weeks, our team works on features and improvements. Then, in the following two weeks, the team works on dependencies, small fixes, upgrades, and planning for future projects.

Our team meets weekly to discuss projects, especially what is blocking or can be discussed. 

We have an onboarding plan for new collaborators. They start with smaller fixes and then gradually move to more complex projects. This helps us avoid speeding up the learning curve process and reduces the possibility of introducing bugs or issues on our environments.

If some definition changes when the development has already started, we sync and update the project to reflect the new state.

### Secure Coding

Starting in 2024, [Latitude.sh](http://Latitude.sh) will apply secure coding training to all developers commiting production code, ensuring everyone understands the possible issues with their code. 

The last test was applied on **29 April 2024**.
<br/><br/>

## Testing

A crucial part of the software development workflow is testing, where other developers and stakeholders validate features and bug fixes before going to production.

We have different environments to reproduce features safely and a rollout strategy to deliver complex features to users, including feature flagging and early access gateways.

### Environments

We define a sandbox environment for every project we create that allows internal teams to test and reproduce exactly what users will experience. It is triggered using a branch model that the projects contain. Developers push changes to a branch and our CD pipeline deploys it into the sandbox environment.

### Pull Request Templates

Each Pull Request has an associated template in Github that nudges developers about specific topics like security, events, and documentation. The template also helps developers create a standardized pull request that is easy to review and covers all points to ensure that changes are applied correctly.

### Culture

Thorough testing is part of our culture. When new developers join [Latitude.sh](http://Latitude.sh), there are plenty of documents about testing that they must read before starting reviewing work from their peers.  The documents cover not only testing but how we develop and enforce how much we care about our users and the stability of our platform. Only approved pull requests with green tests can be merged to production.

On the retrospective meeting after the six weeks cycle we also review how our test process is doing, checking if we are failing and discussing what can be improved. It is important to always review and guarantee that everyone is on the same page.

Our documentation is reflected by the automated tests we create, so it’s important to test the worst scenario and validate if there’s nothing being leaked. Most of the time we spend creating a feature is developing the automated testing scenarios. It is a important step of our testing process.

### When a issue appears

Our team evaluates all the current issues, with different types of view. When critical issues appear, we stop raising anything new and work only to solve the current problem.

Incidents are reported by the team on [status.latitude.sh](https://status.latitude.sh/). Transparency is one of our core values and we take it seriously.
<br/><br/>

## Deployment

The deployment step is created by our team to be as automated as possible. When a pull request is merged, the deployment workflow starts and the code is live in production in around five minutes.

We do not consider a task to be completed before double-checking the behavior in production. This is the most important aspect of QA before a ticket is closed. 

After a review gets approved, the card goes to the QA and the developer needs to test it into the production environment, ensuring that everything is working as expected.

### Access Control

Environment access are restricted by SAML and two factor authentication. SSH keys are provisioned and deprovisioned automatically when collaborators gain and lose access to an environment. For example, when an employee leaves the company and their account is removed, they can no longer access any servers or infrastructure.

We build several internal tools to avoid human interactions within our environments as much as possible.

### Backup

We run on-site and off-site backups daily for all systems and multiple times daily for critical systems. Critical systems have two to three different backup strategies, usually comprised of two vendors (Veeam and Acronis) and one dump-and-store technique. 

We do full backup restoration on air-gapped environments every six weeks and get daily reports and checksums.

### Documentation

Documentation is a huge part of our product and culture. Therefore all projects need an associated documentation. Our team maintains a wiki with all of the projects documentation and technical decisions.
<br/><br/>

## Onboarding and Training

When a collaborator joins [Latitude.sh](http://Latitude.sh), they spend a few weeks learning about how we work and understanding how we collaborate and build products. We collaborate between multiple teams and create new trainings. It is challenging ensuring that everyone understands the changes that company has been working on as it grows, but we take it seriously.

There are different types of trainings that we are currently applying to developers:

- Onboarding: Product, how we work, collaboration and ceremonies;
- General Continuous Security Training: Applied to the whole company;
- Security Development: Applied to the developers annually;
