[200~Postmortem: Web Stack Debugging Issue on August 23, 2024

Issue Summary
Duration:
August 23, 2024, 10:30 AM - 12:15 PM EAT (1 hour 45 minutes)
Impact:
During the outage, 85% of users experienced slow page load times or complete inaccessibility when trying to access our main application. The remaining 15% of users encountered intermittent issues. The service affected was the user authentication API, which caused a cascade of issues throughout the application.
Root Cause:
The root cause was a misconfiguration in the load balancer that led to uneven distribution of traffic. This resulted in one of the servers being overwhelmed, causing a high number of failed requests and slow responses.

Timeline
10:30 AM - Issue detected through monitoring alert showing a spike in failed authentication requests.
10:35 AM - Initial investigation began focusing on the authentication service database, suspecting a possible connection pool issue.
10:45 AM - Database queries were ruled out as a potential cause; attention shifted to network latency checks.
11:00 AM - Misleading path taken: Investigated potential external DDoS attack due to unusual traffic patterns.
11:15 AM - Escalated to the DevOps team after ruling out external factors.
11:30 AM - Load balancer configuration reviewed; identified uneven traffic distribution to servers.
11:45 AM - Load balancer configuration was updated to distribute traffic evenly across all servers.
12:00 PM - System performance restored; monitoring continued to ensure stability.
12:15 PM - Officially declared the incident resolved.

Root Cause and Resolution
Root Cause:
The issue was caused by a misconfiguration in the load balancer settings, where the weight assigned to one of the servers was disproportionately higher than the others. This caused one server to handle the majority of the traffic, leading to it becoming overwhelmed and resulting in slow or failed responses.
Resolution:
The resolution involved reconfiguring the load balancer to distribute traffic evenly across all servers. After identifying the misconfiguration, the DevOps team adjusted the weight settings for each server, ensuring an even distribution of incoming requests. This change allowed the overwhelmed server to recover and restored normal service levels.

Corrective and Preventative Measures
Improvements/Fixes:
Implement more comprehensive monitoring on load balancer traffic distribution to detect uneven patterns earlier.
Conduct a thorough review of current load balancer configurations and correct any inconsistencies.
Improve alert specificity to reduce time spent on misleading investigation paths.
Tasks to Address the Issue:
Patch Load Balancer Configuration: Review and adjust the load balancing algorithm to ensure even traffic distribution.
Add Monitoring on Traffic Distribution: Implement alerts for uneven traffic distribution across servers.
Review Server Capacity: Perform load testing on all servers to ensure they can handle maximum traffic capacity.
Improve Documentation: Update internal documentation to include specific steps for troubleshooting similar load balancer issues in the future.
Team Training: Conduct a training session for engineers on effective load balancer management and troubleshooting.

