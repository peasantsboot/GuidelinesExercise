# Integration Flow Design Guidelines for Exactly Once delivery

## Overview

As an integration developer, you need to make sure that you design integration flows in a robust fashion in order to safeguard your company's mission-critical business processes. The [Integration Flow Design Guidelines](https://help.sap.com/docs/integration-suite/sap-integration-suite/integration-flow-design-guidelines) help to design enterprise-grade integration flows on the Cloud Integration capability of SAP Integration Suite. They cover different aspects such as resource handling, better readability, security, error handling, etc. In addition, the most common Enterprise Integration Patterns are provided. As part of the patterns, we also provide guidelines about how to implement Quality of Service Exactly Once.

This session focuses on the Exactly Once guidelines applying different capabilities that allow to implement Exaclty Once delivery in Cloud Integration such as ID mapper and idempotent process calls.

## Access to SAP Integration Suite tenant

For running through the exercises, you need access to an SAP Integration Suite tenant.

- Please use this [**SAP Integration Suite tenant**](https://cpisuite-europe-03.integrationsuite.cfapps.eu20-001.hana.ondemand.com/shell/home) for your exercises.
- Use the user **userXX** with **XX** your ID and password provided by the instructors.

## Exercises

In the following, the complete list of exercise steps are listed. You can use this section as an index or table of contents. Use the breadcrumb navigation on top of the pages to go back to the Table of Contents.

If you are new to SAP Integration Suite, start with the first exercise. This shows you how to navigate within most of the SAP Integration Suite capabilities. Otherwise, if you are already experienced with SAP Integration Suite, you may skip this part.

- [Exercise 1 - Explore SAP Integration Suite (optional)](exercises/ex1/)
- [Exercise 1 - Exactly Once scenario with receiver not being idempotent](exercises/ex2/)
- [Exercise 2 - Extend the Exactly Once scenario with Splitter step](exercises/ex3/)

<!-- **OR** Link to the Tutorial Navigator for example... 
Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).
-->

<!--
**IMPORTANT**
Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 
-->

<!--
## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.
-->

## Code of Conduct
1. Use the tenant that we provide only for this exercise, and not for anything else. For further exploration of Migration Assessment and Cloud Integration, use a free BTP trial account or a Free Tier tenant.
2. Do not share any private or personal information such as your name, email address or affiliation.
3. Please strictly follow the instructions, regarding the naming conventions you will use to name the artifacts you will create. This ensures that you will be able to successfully complete the tasks, without clashing with other participants.
4. Other artifacts, created by other participants, will appear in your shared account. Do not access or delete these artifacts. Please respect the rules and allow others to have the same learnings as you.

Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support
Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
