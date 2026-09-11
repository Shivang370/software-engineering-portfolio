# [Project : Automyze Decomissioning]

Unleash is a feature management platform designed for progressive delivery and controlled feature rollouts. It enables teams to:
    * Toggle features on/off without redeploying code.
    * Perform gradual rollouts, A/B testing, and targeted releases.
    * Control feature availability based on:
        * Session attributes
        * Custom strategies (like time-based toggles, geo-location, etc.)

## Core Benefits:
* Improved deployment safety with gradual rollouts.
* Reduced risk through targeted exposure.
* Decouples deployment from feature release.
* Central dashboard to manage and monitor feature toggles.

# [GitHub Repository Name : dip-lib-instrument-feature-flags]

## Overview

The dip-lib-instrument-feature-flags library is a reusable Java wrapper designed to simplify feature flag evaluation in microservices by integrating with the Unleash SDK. It encapsulates the complexity of interacting with the Unleash feature flag system and provides a consistent, lightweight interface for enabling or disabling features dynamically across distributed services.
This library enables other microservices to:
    * Query feature flag status using simple, abstracted methods.
    * Perform flag and context-based flag evaluation (e.g., userId, IP, session, custom context-fields).
    * Log evaluation events and failures uniformly.
    * Ensure feature toggling is decoupled from business logic


## What problem does unleash solves ?

In modern microservices-based applications, releasing new functionality can be risky because deploying code and exposing features to users happen simultaneously. If an issue is discovered after deployment, teams often need to perform rollbacks, which can be time-consuming and disruptive. Unleash solves this problem by decoupling deployment from feature release.

Key Problems Addressed by Unleash

1.⁠ ⁠Reducing Deployment Risk Traditionally, new features become available as soon as code is deployed. If a feature contains bugs or causes performance issues, the entire deployment may need to be rolled back. Unleash allows teams to keep new features disabled after deployment and enable them only when they are ready, significantly reducing release risk.

2.⁠ ⁠Enabling Gradual and Controlled Rollouts Releasing a feature to 100% of users at once can expose the entire customer base to potential issues. Unleash enables gradual rollouts, allowing teams to release features to a small percentage of users first, monitor behavior, and progressively increase exposure.

3.⁠ ⁠Supporting Targeted Feature Availability Different users often require different experiences. Unleash allows teams to enable features based on user attributes, session data, country, IP address, environment, customer segments, or custom business rules, enabling personalized and controlled releases.

4.⁠ ⁠Accelerating Experimentation and Validation Organizations often need to validate new ideas before a full launch. Unleash supports A/B testing and canary releases by selectively exposing features to specific user groups, helping teams gather feedback and make data-driven decisions.

5.⁠ ⁠Eliminating Frequent Code Changes for Feature Control Without a feature management platform, enabling or disabling functionality often requires code modifications and redeployments. Unleash provides centralized feature control, allowing teams to manage feature availability dynamically without changing application code.

6.⁠ ⁠Improving Operational Resilience If a newly released feature causes production issues, teams can immediately disable the feature through Unleash without triggering an application rollback. This acts as a safety switch and minimizes customer impact.

How dip-lib-instrument-feature-flags Helps :

While Unleash provides the feature management platform, the dip-lib-instrument-feature-flags library simplifies integration with Unleash across microservices by:

    * Abstracting direct interactions with the Unleash SDK.
    * Providing a standardized API for feature flag evaluation.
    * Supporting context-aware evaluations (userId, session, IP, custom context fields).
    * Centralizing logging and error handling.
    * Keeping feature toggle logic separate from business logic.
    * Ensuring consistency across distributed services.


## Architecture

![alt text](image.png)

## Technology Stack

•⁠  ⁠[Java]
•⁠  ⁠[Common-Library] published as an artifact library in aacom
•⁠  ⁠[Postgres] database used by unleash internally
•⁠  ⁠[Azure]
•⁠  ⁠[Junit/Mockito]

## Steps to use

* Use dip-lib-instrument-feature-flags 1.0.5+ version, import in build.gradle file. 
implementation 'com.theaa.dip:instrument-feature-flags:1.0.5+'
* Add @EnableFeatureFlags annotation in the main application.
* Autowire the FeatureFlagUtils class in service & use isFeatureEnabled(“flagName”), isFeatureEnabled(“flagName”,context) as per use case. Also add the context in the Unleash UI for context-field matching. Note : userId, ipAddress, sessionId are default names for context-field as defined in dip-lib-instrument-flags, any other custom context-fields can be passed in the isFeatureEnabled() & configured from Unleash UI.
* Unleash url, token as per environment, toggle interval & app-name for checking feature-flag usage are configured as a part of ssm parameters in AWS System Manager.

References : Detailed documentations were prepared along with use cases.

## Testing

Junit Test cases covering various scenarios followed by qa validation and regression testing.

## Requisites and Challenges

Implementing Unleash Enterprise required both technical and organizational considerations. One of the primary prerequisites was procuring and onboarding a hybrid Unleash Enterprise license that could support feature flag management across multiple environments and services.

A key challenge was establishing a consistent feature flag strategy across different environments (DEV, QA, UAT, and PROD) while ensuring proper governance and preventing configuration drift. The team also had to become familiar with the Unleash dashboard, feature toggle lifecycle management, rollout strategies, and operational processes for enabling or disabling features as business needs evolved.

Another important aspect was implementing role-based access control, as feature flag management needed to be restricted to a limited set of authorized users across multiple teams. This required defining ownership, access boundaries, approval processes, and operational guidelines to ensure that feature toggles were managed securely and consistently.

Additionally, maintaining feature parity across environments, tracking flag usage and cleanup, and coordinating rollouts among dependent microservices posed ongoing challenges. Success depended on clear governance, proper documentation, and close collaboration between development, operations, and product teams to ensure controlled and reliable feature releases.

Key Challenges:

Procuring and onboarding a hybrid Unleash Enterprise license.
Managing feature flags consistently across DEV, QA, UAT, and PROD environments.
Gaining familiarity with the Unleash dashboard and rollout strategies.
Ensuring timely feature enablement/disablement without redeployments.
Restricting dashboard access to authorized users through role-based controls.
Defining ownership and governance for feature flag management across teams.
Preventing configuration drift and maintaining environment-level consistency.
Tracking stale flags and ensuring proper feature flag lifecycle management.
