---
layout: post
permalink: "/post/software-engineering/all-about-logic-app-p1"
title:  "Embracing Low Code/No Code with Azure Logic Apps"
---

I miss the good ol' days when coding was all about slicing and dicing lines of code. These days, everything's about the rage of generative AI and workflows (low-code/no-code platforms). Not that I’m complaining, it's just technology have progressed so much where we don't have to write hundreds-thousands lines of code to get things done. 

In this blog, I’ll dive into Microsoft Azure’s low-code/no-code offering—Azure Logic Apps.

Sidenote: If you’re wondering, "Why not Power Automate?" 
You can check out this <a href="https://learn.microsoft.com/en-us/microsoft-365/community/power-automate-vs-logic-apps">Microsoft doc</a> for the full breakdown. 
Long story short: Power Automate is more about Office 365, while Logic Apps is for when you want to get serious with enterprise-level integrations.


Quick setting of expectation, I will be going through the Azure portal so we assume management of the service will be done through clickOps. We will talk about IaC management on the next blog.

### Agenda:
1. Provisioning: What to Expect When Spinning Up a Logic App
2. Exploring the Menu Blades: IAM, Environment Variables, Diagnostic Settings, and More
3. Diving into the Logic App Designer: Where the Magic (or Madness?) Happens
4. Resources

<br/>

### Provisioning: What to Expect

When you're spinning up a Logic App, one of the first things to consider is the hosting option. <br/>
There are two categories to choose from: `Consumption` and `Standard`.

<img src="/assets/logicapp-1.png" alt="LogicApp">

#### Short breakdown
1. Consumption:
    - Tenancy: Muli-tenant
    - Networking: Public cloud
    - Connector: Built-In only
    - Pricing: Per operation/workflow trigger/execution
    - Workflow: Single workflow only
2. Standard: 
    - Workflow Service Plan:
        - Tenancy: Dedicated / Single-tenant
        - Networking: Supports VNET Integration
        - Connector: Built-In + (supports) In-App and Custom connector
        - Pricing: Based on the hosting pricing tier
        - Workflow: Supports multiple workflows (stateful/stateless)
    - ASEv3 (App Service Environment):
        - Tenancy: Dedicated / Single-tenant
        - Networking: Full isolation / VNET Integration
        - Pricing: Per App Service Plan for ASE instance
        - Workflow: Supports multiple logic apps and workflows (stateful/stateless)
    - Hybrid:
        - This is new and still in preview. <br/> Haven't really personally tried and used this but based on this <a href="https://learn.microsoft.com/en-us/azure/logic-apps/create-standard-workflows-hybrid-deployment?tabs=azure-portal"> Microsoft doc</a>, it's purpose is to leverage existing infrastructure you may have whether it's on-prem or in private/public cloud.
        - One thing to note is the <a href="https://learn.microsoft.com/en-us/azure/logic-apps/create-standard-workflows-hybrid-deployment?tabs=azure-portal#limitations"> limitation</a> around this. 


#### Supply parameters

*Consumption:*

    Basics: Resource details
        - Subscription: Select your Azure subscription
            - Resource Group: Choose your existing resource group or create a new one
        - Instance Details:
            - Logic App Name: Name your Logic App
            - Region: Select the Azure region where the Logic App will be hosted
            - Enable Log Analytics: Optionally enable for logging and monitoring
    Tags: Name-value pair for categorizing your resource
    Review + create: Validation of your selections and creation of the Logic App


<img src="/assets/logicapp-2.png" alt="LogicApp">

<br/>

*Standard:*

    Workflow Service Plan

    Basics: Resource details
        - Subscription: Select your Azure subscription
            - Resource Group: Choose your existing resource group or create a new one
        - Instance Details:
            - Logic App Name: Name your Logic App
            - Region: Select the Azure region where the Logic App will be hosted
            - Windows Plan: Choose an App Service Plan for hosting your standard logic app
        - Zone Redundancy:  Optional for high availability across availability zones
    Storage: 
        - Storage type: Select the type of storage Azure Storage or SQL (Preview) + Azure Storage for workflow data
        - Storage account: Choose or create a Storage Account to store logs and other data
        - Diagnostic Settings: Enable for logging and performance tracking
    Networking: Optional VNET integration for secure network communication
    Monitoring: Optional for tracking workflow performance and failures
    Tags: Name-value pair for categorizing your resource
    Review + create: Validation of your selections and creation of the Logic App

<img src="/assets/logicapp-3.png" alt="LogicApp">

<br/>

ASEv3 (App Service Environment)

The parameters for ASEv3 Logic App is similar to the Workflow Service Plan, but before supplying, you must first provision an ASEv3 and select it under the *Windows Plan* option.

    App Service Environment:

    Basics: Resource details
        - Subscription: Select your Azure subscription
            - Resource Group: Choose your existing resource group or create a new one
        - Instance Details:
            - App Service Environment Name: Name your ASE
            - Virtual IP: Select between Internal or External
            - Region: Choose the region where the ASE will be hosted
    Hosting:
        - Hardware isolation: Enable isolation for dedicated hardware
        - Zone redundancy: Optional for high availability across availability zones
    Networking:
        - Virtual Network: Choose the virtual network to integrate
        - Subnet: Select a subnet for your ASE
        - DNS: Specify DNS settings for name resolution
        - Inbound IP address: Configure the inbound IP address for accessing the ASE
    Tags: Name-value pair for categorizing your resource
    Review + create: Validation of your selections and creation of the Logic App

<img src="/assets/logicapp-4.png" alt="LogicApp">

##### Note: Deployment takes around 2 hours - 4 hours

<br/>


*Hybrid - I'll have to further explore and will create a separate blog for this to see it in action.*

<br/>

### Exploring the Menu Blades

What you'll see in a <b>Consumption</b> Logic App:
1. <b> Overview </b> - Provides a high-level summary which includes status, history, and quick actions. 
2. <b>Activitity log</b> - Shows a detailed log of all activities and operations.
3. <b>Access control (IAM)</b> - Manages permissions and roles.
4. <b>Tags</b> - Allows adding metadata through name-value pairs to organize and categorize resources.
5. <b>Diagnose and solve problems</b> - Provides troubleshooting tools and guided solutions for common issues.
6. <b>Development Tools</b>
    - <b>Logic App designer</b> - Visual interface for building and managing workflows.
    - <b>Logic app code view</b> - Allows direct editing of the underlying JSON code.
    - <b>Logic app templates</b> - Provides pre-built templates to accelerate Logic App creation.
    - <b>Run history</b> - Displays a history of all workflow runs, including status and execution details.
    - <b>Versions</b> - Tracks and manages different versions of the Logic App workflow.
    - <b>API connections</b> - Shows the connections used by the Logic App to external services.
    - <b>Quick start guides</b> - Provides documentation and tutorials for getting started with Logic Apps.
7. <b>Settings</b>
    - <b>Settings</b> - Configure general settings, including runtime configuration and workflow settings.
    - <b>Authorization</b> - Manages authentication and authorization policies.
    - <b>Access Keys</b> - Provides keys and credentials for secure access
    - <b>Identity</b> - Configures the managed identity for accessing other Azure resources securely.
    - <b>Properties</b> - Displays detailed properties, including resource IDs and endpoints.
    - <b>Locks</b> -  Prevents unintended changes or deletions to the Logic App through resource locking.
8. <b>Monitoring</b>
    - <b>Tasks </b> - Shows scheduled and running tasks associated with the Logic App.
    - <b>Export template</b> - Generates an ARM template for deploying the Logic App in different environments.
9. <b>Help</b>
    - <b>Changelog</b> - Displays updates and changes made to the Logic App.
    - <b>Support + Troubleshooting</b> - Provides links to support resources and troubleshooting tools.

<img src="/assets/logicapp-6.png" alt="LogicApp">

<br/>

What you'll see in a <b>Standard - Workflow Service Plan</b> Logic App:
1. <b> Overview </b> - Same with Consumption
2. <b> Activity log </b> - Same with Consumption
3. <b> Access control (IAM) </b> - Same with Consumption
4. <b> Tags </b> - Same with Consumption
5. <b> Diagnose and solve problems </b> - Same with Consumption
6. <b> Microsoft Defender for Cloud </b>  - Provides security recommendations and threat protection
7. <b> Events (preview) </b> - Displays events related to your Logic App, including triggers and runs.
8. <b> Recommended services (preview) </b> Suggests Azure services to enhance functionality.
9. <b> Log stream </b> - Shows real-time logs for monitoring your Logic App's behavior and troubleshooting.
10. <b> Workflows </b>
    - <b>Workflows</b> - Manage and view individual workflows
    - <b>Connections</b> - Configure API connections used by your workflows.
    - <b>Parameters</b> - Manage global parameters for use in workflows.
11. <b> Artifacts </b>
    - <b>Schemas</b> - Manage XML schemas for workflow validation.
    - <b>Maps</b> - Create and manage data transformation maps.
    - <b>Assemblies</b> - Upload and manage custom .NET assemblies.
    - <b>Rules</b> - Configure business rules for workflow automation.
12. <b> Deployment </b>
    - <b>Deployment slots</b> - Manage deployment environments for testing and production.
    - <b>Deployment Center</b> - Set up continuous deployment from repositories like GitHub or Azure DevOps.
13. <b> Settings </b>
    - <b>Environment variables</b> - Configure variables accessible within the app.
    - <b>Configuration</b> - Manage application settings and connection strings.
    - <b>Authentication</b> - Set up authentication options for security.
    - <b>Identity</b> - Manage the managed identity for accessing other Azure resources.
    - <b>Backups</b> - Configure and manage backup settings.
    - <b>Custom domains</b> - Add and manage custom domain names.
    - <b>Certificates</b> - Manage SSL/TLS certificates for secure communication.
    - <b>Networking</b> - Configure network settings, including VNET integration.
    - <b>Scale up (App Service plan)</b> - Increase the instance size or pricing tier.
    - <b>Scale out (App Service plan)</b> - Increase the number of instances for load balancing.
    - <b>Service Connector</b> - Set up secure connections to other Azure services.
    - <b>Properties</b> - View general information, including ID and status.
    - <b>Locks</b> - Apply resource locks to prevent accidental changes or deletions.
14. <b> App Service plan </b>
    - <b>App Service plan</b> - Manage the hosting service plan.
15. <b> Development Tools </b>
    - <b>Advanced Tools</b> - Access tools like Kudu for advanced diagnostics and management.
16. <b> API </b>
    - <b>CORS</b> - Configure Cross-Origin Resource Sharing (CORS) policies for API access.
17. <b> Monitoring </b>
    - <b>Insights</b> - Gain insights into performance and health.
    - <b>Alerts</b> - Create and manage alerts for specific conditions.
    - <b>Metrics</b> - Monitor performance metrics.
    - <b>Advisor recommendations</b> - Get optimization suggestions from Azure Advisor.
    - <b>Health check</b> - Monitor the health status of the app.
    - <b>Application Insights</b> - Enable deep performance monitoring and diagnostics.
    - <b>Logs</b> - View and query log data for troubleshooting and analysis.
    - <b>Diagnostic settings</b> - Configure where to send logs and metrics, like Log Analytics or Storage.
    - <b>App Service logs</b> - Enable and view logging for activities.
18. <b> Automation </b>
    - <b>Tasks</b> - Same with Consumption
    - <b>Export template</b> - Same with Consumption
19. <b> Support + Troubleshooting </b>
    - <b>Resource health</b> - Check health status and identify potential issues.
    - <b>Support + Troubleshooting</b> - Same with Consumption

<img src="/assets/logicapp-7.png" alt="LogicApp">

<br/>

What you'll see in a <b>Standard - ASEv3</b> Logic App:

### Let's dive into each Blade

##### Note: "Note: I'll start with Consumption, then move to Standard.

#### Overview

This blade provides a high-level summary of your Logic App's current status and functionality. 

It displays key details such as the `Definition` (workflow design) and *Status* (active or disabled). And it also highlights useful insights through `Runs History`, `Trigger History`, and `Metrics`, helping you monitor and troubleshoot your Logic App effectively.

At the top of the Overview, you’ll find quick actions like:

`Run`: Manually trigger your Logic App. <br/>
`Edit`: Open the Logic App Designer to modify your workflow. <br/>
`Delete`: Permanently remove the Logic App. <br/>
`Disable`: Pause the Logic App without deleting it.<br/>
`Clone`: Create a copy of the Logic App, this is useful for testing or versioning.

<img src="/assets/logicapp-5.png" alt="LogicApp">


#### Activity log

This blade provides detailed logs of all the activities and operations related to your Logic App. <br/>
It allows you to track actions such as who initiated the activity, when it occurred, and its outcome. <br/>
Key details include `Event Types`, `Operation Name`, and `Status`. This helps you monitor the performance and diagnose any issues.

It also provides useful filters to narrow down results, such as `Subscription`, `Time Range`, and `Event Types`, along with an option to export the data for further analysis.

<img src="/assets/logicapp-8.png" alt="LogicApp">


#### Access control (IAM)

This blade provides a centralized place to manage user and service permissions. <br/>
It allows you to define who has access to your Logic App and what actions they can perform.

Key features include:

- Check Access: View access details for users and resources, helping you understand who can access the Logic App and their permissions.
- View my access: See what access you have to resources in the subscription.
- Check access: Check the access level of a specific user or service principal.
- Role Assignments: Review and manage roles assigned to users, groups, and applications, specifying who has access to your Logic App and the level of access granted.
- Roles: List and manage built-in roles or custom roles that define what users can do within the Logic App.
- Deny Assignments: Control explicit deny assignments for users and groups to ensure they cannot access specific resources.
- Classic Administrator: Manage legacy access settings and user roles under the classic model.

This blade helps ensure proper security and compliance by restricting access to authorized entities only.

<img src="/assets/logicapp-9.png" alt="LogicApp">

#### Tags

This blade allows you to manage metadata associated with your Logic App for organizational and categorization purposes.

<img src="/assets/logicapp-10.png" alt="LogicApp">

##### Note: Tags are useful for filtering resources in large environments and enabling easier management and cost tracking

#### Diagnose and solve problems

This blade provides tools and insights to help troubleshoot issues and improve the performance of your Logic App. <br/>

<img src="/assets/logicapp-11.png" alt="LogicApp">

It offers automated diagnostics, common solution suggestions, and step-by-step guidance for identifying and resolving potential problems efficiently.

### Development Tools

#### Logic app designer

This blade is where the magic (or madness?) happens!
It's where you visually design and configure your workflows.

It allows you to build, edit, and manage the logic behind your app by adding triggers, actions, and connectors in a user-friendly, drag-and-drop interface.

Key features:
- Triggers: The starting point of your workflow, typically an event or condition that initiates the Logic App
- Actions: These are steps/operation that happen after the trigger, such as sending emails, creating records, or calling other APIs.
- Connectors: Pre-built integrations with various services that allow you to easily connect your Logic App to internal/external systems.

These key features are central to building, testing, and managing workflows effectively within the Logic App Designer.

<img src="/assets/logicapp-12.png" alt="LogicApp">

We'll dive even deeper later on and also include best practices.


#### Logic app code view

This blade contains the workflow definition in *JSON* format.
It allows you to view and edit the raw code behind the Logic App, offering a more granular approach compared to the visual designer.

Key features:
- JSON representation: Displays the entire workflow in code, which enables control over the structure.
- Edit workflow directly: Allows you to modify the workflow logic manually by editing the JSON.
- Save and deploy: After editing the code, you can save and deploy the updated logic.

<img src="/assets/logicapp-13.png" alt="LogicApp">

This is useful for advanced users who need to fine-tune or directly manipulate the underlying workflow code.

#### Logic app templates

This blade offers a collection of pre-built templates designed to help you quickly create workflows for common scenarios.
These templates are provided by Azure and the community.

<img src="/assets/logicapp-14.png" alt="LogicApp">

This is a great way to get started quickly, especially if you want to automate common processes without building everything from scratch!

#### Run History

This blade provides a detailed log of past executions which helps you monitor and troubleshoot the workflow runs.

<img src="/assets/logicapp-15.png" alt="LogicApp">

This is essential for debugging and helps you analyze optimization for workflow performance.

#### Versions

This blade keeps track of all previously saved versions of your Logic App, allowing you to review, compare, and restore earlier configurations.

<img src="/assets/logicapp-16.png" alt="LogicApp">

This is useful for version control and troubleshooting unintended changes.

#### API Connections

This blade displays and manages all the connections your Logic App uses to integrate with external services.

<img src="/assets/logicapp-17.png" alt="LogicApp">

This is essential for maintaining seamless integrations with external systems.


#### Quick start guides

This blade provides helpful resources to get started with Logic Apps efficiently.

<img src="/assets/logicapp-18.png" alt="LogicApp">

This accelerates beginners that are looking to explore Logic Apps further.


### Settings

#### Settings

This blade provides key configuration options for security, integration, and performance tuning.

Configurations include:

- <b>Access control</b>: Restrict inbound calls to triggers based on specific IP ranges.
- <b>Integration Account</b>: Connect to an Integration Account for enhanced B2B capabilities.
- <b>Runtime Options</b>: Enable *High Throughput* Mode (preview) for improved performance.
- <b>Run History Retention</b>: Configure how long run history data is stored (preview).

<img src="/assets/logicapp-19.png" alt="LogicApp">

This controls help secure and optimize your logic app's execution.

#### Authorization

This blade allows you to configure Azure Active Directory (AAD) Authorization Policies to control access.

<img src="/assets/logicapp-20.png" alt="LogicApp">

This ensures that only authenticated users or services with the right permissions can trigger the Logic App.

#### Access keys

This blade provides authentication keys that allow external services or applications to securely call the Logic App’s HTTP triggers.

Primary and Secondary Access keys can be used to authenticate API requests without needing Azure Active Directory (AAD).

<img src="/assets/logicapp-21.png" alt="LogicApp">

#### Identity

This blade allows you to manage the identities that the Logic App uses to interact with other Azure resources securely.

- <b>System Assigned</b>: This identity is used to authenticate with Azure resources without requiring explicit credentials.
- <b>User Assigned</b>: While this identity allows you to assign an existing Azure Managed Identity to the Logic App, giving you more control over its lifecycle and permissions.

<img src="/assets/logicapp-22.png" alt="LogicApp">

#### Properties

This blade helps you view configuration details about your Logic App, such as its resource ID, location, and other metadata.

#### Locks

This blade allows you to prevent accidental deletion or modification of your Logic App by applying management locks.

- <b>Read-only</b>: Prevents modifications to the Logic App by restricting write operations.
- <b>Delete</b>: Prevents deletion of the Logic App, ensuring it remains intact.

<img src="/assets/logicapp-23.png" alt="LogicApp">

These locks help safeguard critical resources by ensuring that no unintended changes or deletions can occur.


### Monitoring

#### Alerts

This blade allows you to set up notifications for specific events or conditions within the Logic App.

Key features:

- <b>Create Alert</b>: Set conditions that trigger alerts, such as failures, errors, or other specific events in the Logic App.
- <b>Alert Rules</b>: Define rules based on metrics, activity logs, or custom criteria.
- <b>Notification Channels</b>: Choose how to receive alerts (e.g., email, SMS, webhooks, etc.).

<img src="/assets/logicapp-24.png" alt="LogicApp">

This will help you stay informed about a wide range of conditions or failures, ensuring prompt action can be taken when needed.

#### Metrics

This blade allows you to view and analyze the performance of your Logic App using various metrics.

<img src="/assets/logicapp-25.png" alt="LogicApp">

It helps you monitor your Logic App's performance and identify trends or issues that may need attention.

#### Diagnostic settings

This blade enables you to configure and manage logging and monitoring for your Logic App.

Key features:

- <b>Log Configuration</b>: Enable logging to capture detailed information about Logic App runs, failures, and performance.
- <b>Destination Setup</b>: Choose where to send the logs, such as Azure Monitor, Log Analytics, or Event Hubs.
- <b>Custom Metrics</b>: Optionally configure custom logging for specific events or actions within your Logic App.

<img src="/assets/logicapp-26.png" alt="LogicApp">


<img src="/assets/logicapp-27.png" alt="LogicApp">

This ensures that you can track the health and performance of your Logic App and troubleshoot issues effectively using comprehensive diagnostic data.

#### Diagnostic settings

This blade allows you to view detailed logs related to your Logic App's execution and performance.

<img src="/assets/logicapp-28.png" alt="LogicApp">

It helps you monitor the execution and troubleshoot any issues by providing in-depth logging information.

#### Diagnostics

This blade serves as a dashboard for monitoring your Logic App's performance and health.

<img src="/assets/logicapp-29.png" alt="LogicApp">

This allows you to easily monitor the performance of your Logic App and take action based on the collected diagnostics.

### Automation

#### Tasks 

This blade enables you to automate common management actions and workflows.

<img src="/assets/logicapp-30.png" alt="LogicApp">

Setting up tasks helps streamline routine operational procedures which reduces manual effort and improves efficiency.

#### Export Template

This blade allows you to generate an ARM (Azure Resource Manager) template that captures your Logic App’s current configuration.

Key features:

- <b>Generate Template</b>: Creates a JSON file representing your Logic App’s structure and settings.
- <b>Customize and Reuse</b>: Modify the template to fit other environments or scenarios.
- <b>Deploy Consistently</b>: Use the template to redeploy the Logic App in different resource groups or subscriptions, ensuring consistent setups.

<img src="/assets/logicapp-31.png" alt="LogicApp">

This is handy for automation, backups, and replicating your Logic App across environments.

### Help

#### Changelog

This blade provides a record of updates and improvements made to the Logic App service over time.

<img src="/assets/logicapp-32.png" alt="LogicApp">

This ensures you’re always aware of the latest improvements and fixes.


#### Support + Troubleshooting

This blade provides essential tools to help diagnose issues and get assistance when needed.

<img src="/assets/logicapp-33.png" alt="LogicApp">

It ensures that you have the right resources to quickly diagnose, troubleshoot, and escalate issues when necessary.

