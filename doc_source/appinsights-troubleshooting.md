# View and troubleshoot problems detected by Amazon CloudWatch Application Insights for \.NET and SQL Server<a name="appinsights-troubleshooting"></a>

An overview of problems impacting your \.NET and SQL Server applications is listed under the CloudWatch Application Insights for \.NET and SQL Server widget in the default overview page of the CloudWatch console\. For more information, see [Getting started with Amazon CloudWatch Application Insights for \.NET and SQL Server](appinsights-getting-started.md)\.

The CloudWatch Application Insights for \.NET and SQL Server widget displays the following:
+ The severity of the problems detected
+ A summary of the problem
+ The possible root cause of the problem
+ The time the problem started
+ The resolution status of the problem
+ The affected Resource Group

To drill down into details of a specific problem, under **Problem Summary**, select the description of the problem\. A detailed dashboard displays insights into the problem and related metric anomalies and snippets of log errors\. From here, you can provide feedback on the relevance of the insight by selecting whether it is useful\.

If a new, unconfigured resource is detected, the problem summary description takes you to the **Edit configuration** wizard to configure your new resource\. If needed, you can view or edit your Resource Group configuration by choosing **View/edit configuration** in the upper right‐hand corner of the detailed dashboard\.

To return to the overview, choose **Back to overview**, which is next to the CloudWatch Application Insights for \.NET and SQL Server detailed dashboard header\.

**Information Provided About Detected Problems**

CloudWatch Application Insights for \.NET and SQL Server provides the following information about detected problems:
+ A short summary of the problem
+ The start time and date of the problem
+ The problem severity: High/Medium/Low
+ The status of the detected problem: In‐progress/Resolved
+ Insights: Automatically generated insights on the detected problem and possible root cause
+ Feedback on insights: Feedback you have provided about the usefulness of the insights generated by CloudWatch Application Insights for \.NET and SQL Server
+ Related observations: A detailed view of the metric anomalies and error snippets of relevant logs related to the problem across various application components

**Feedback**

You can provide feedback on the automatically generated insights on detected problems by designating them useful or not useful\. Your feedback on the insights, along with your application diagnostics \(metric anomalies and log exceptions\), are used to improve the future detection of similar problems\.

## Configuration errors<a name="appinsights-configuration-errors"></a>

CloudWatch Application Insights for \.NET and SQL Server uses your configuration to create monitoring telemetries for the components\. When Application Insights detects an issue with your account or your configuration, information is provided in the **Remarks** field about how to resolve the configuration issue for your application\. 

The following table shows suggested resolutions for specific remarks\.


| Remarks | Suggested Resolution | Additional notes  | 
| --- | --- | --- | 
|  The quota for alarms has already been reached\.  |  By default, each AWS account can have 5,000 CloudWatch alarms per AWS Region\. See [CloudWatch Limits](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_limits.html)\. When throttled by this limit, CloudWatch Application Insights for \.NET and SQL Server cannot create all of the required alarms to monitor your application\. To resolve this, raise the account limit for CloudWatch alarms\.  | n/a | 
|  The quota for CloudFormation has already been reached\.  |  Application Insights creates one CloudFormation stack for each application to manage CloudWatch agent installation and configuration for all application components\. By default, each AWS account can have 200 stacks\. See [AWS CloudFormation Limits](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html)\. To resolve this, raise the limit for CloudFormation stacks\.  | n/a | 
|  No SSM instance role on the following instances\.  |  For Application Insights to be able to install and configure CloudWatch agent on application instances, AmazonSSMManagedInstanceCore and CloudWatchAgentServerPolicy policies must be attached to the instance role\.   |  Application Insights calls the SSM [DescribeInstanceInformation API](https://docs.aws.amazon.com/systems-manager/latest/APIReference/API_DescribeInstanceInformation.html) to get the list of instances with SSM permission\. After the role is attached to the instance, it takes time for SSM to include the instance in the DescribeInstanceInformation result\. Until SSM includes the instance in the result, NO\_SSM\_INSTANCE\_ROLE error remains present for the application\.  | 
|  New components may need configuration\.  |  Application Insights detects that there are new components in the application Resource Group\. To resolve this, configure the new components accordingly\.  | n/a | 