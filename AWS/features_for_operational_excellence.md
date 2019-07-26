# Features for Operational Excellence

## AWS Well-Architected Framework

- Operational Excellence

- Security

- Reliability

- Performance Efficiency

- Cost Optimization

### six design principles for operational excellence

- **Perform operations as code**: Attempt to code as much of your AWS implementation and operation as possible. Remember that your entire architecture and operations should be “code-able”; this reduces or even eliminates the human error factor.

- **Create annotated documentation**: Automate the creation of annotated documentation of your environment.

- **Make changes small and frequent and reversible**: Design your system so that regular updates are possible, ensure that changes can be small in scope, and ensure that changes can easily be reversed in the event of disaster.

- **Refine operations procedures frequently**: Observe ongoing operations closely and design improvements to evolve the overall system.

- **Anticipate failures**: Be proactive against issues that might occur in your design. Test failure scenarios.

- **Learn from all operational failures**: Share what is learned from any failures.

## PREPARE

### Operational Priorities

- **AWS Cloud Compliance**: Provides valuable information about achieving the highest levels of compliance with various security requirements.

- **AWS Trusted Advisor**: Provides real-time guidance on your AWS operations and helps to ensure you are following best practices. Business Support allows full access to the full set of Trusted Advisor checks.

- **Enterprise Support**: Provides access to Technical Account Managers (TAMs) that can provide guidance on operational excellence.

### Design for Operations

- In your design, include how workloads will be deployed, updated, and operated.

- Implement engineering practices that reduce defects and allow for quick and safe fixes.

- Enable observation with logging, instrumentation, and insightful metrics.

- Design for a code-based implementation and ensure you can also update using code.

- Consider the use of CloudFormation for the construction of version-controlled templates for your infrastructure.

- Set up a Continuous Integration/Continuous Deployment (CI/CD) pipeline using the AWS Developer Tools.

- Apply metadata using tags to help identify resources related to operational activities.

- Design CloudWatch into your system—capture logs, inspect logs, use events.

- Whenever possible, code applications to share metric information with CloudWatch.

- Trace the execution of distributed applications using **AWS X-Ray.**

- When adding instrumentation to workloads, capture a broad set of information to maintain situational awareness.

### Operational Readiness

- Use tools like detailed checklists to know when your workloads are ready for production; use a governance process to make informed decisions regarding launches.

- Use **runbooks** that document routine activities.

- Use **playbooks** that guide processes for issue resolution.

- Ensure enough team members are on staff for operational needs.

- Use as many scripted procedures as possible to foster automation.

- Consider the automatic triggering of scripted procedures based on events.

- Consider scripting routines in the consistent evaluation of your AWS architecture.

- Test failure procedures and the success of your responses.

- Consider parallel environments for testing purposes.

- Use scripting tools and related components like the **AWS Systems Manager Run Command**, **Systems Manager Automation**, and **Lambda**.

- Consider the use of **AWS Config** to help create baselines and then test your configurations through the use of AWS Config rules.

- Encourage team members to constantly further their education on AWS; they can use books like this one and the many free AWS resources found online via the AWS site.

## OPERATE

### Understanding Operational Health

- Track metrics to specific operational business goals.

- Take advantage of the ease with which you can gather and analyze log files. Once again, automate as much as possible through code.

- Create baselines using CloudWatch.

- Use CloudWatch dashboards to create custom views that present system-level and business-level views of metrics.

- Consider the use of Elasticsearch to create dashboards and visualizations of operational health.

- Use the Service Health dashboard to watch for alerts.

- Use the support for third-party log analysis systems such as Grafana, Kibana, and Logstash.

### Responding to Events

- Anticipate for your planned and unplanned events.

- Utilize your runbooks and playbooks.

- Use CloudWatch rules to automatically trigger responses.

- Consider the use of third-party tools for monitoring and automating responses. Some examples are New Relic, Splunk, Loggly, SumoLogic, and Datalog.

- Know when human responses and decisions are needed.

## EVOLVE

### Learning from Experience

- Provide time for the analysis of operations.

- Aggregate and analyze logs.

- Use temporary duplicates of environments for testing when needed.

- Use **CloudTrail to track API activity**.

- Perform cross-team reviews.

### Share Learnings
