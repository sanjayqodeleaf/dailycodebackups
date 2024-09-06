### security steps that can be take to make our k8 infra more secure

- Enable Kubernetes Role-Based Access Control (RBAC)

-  Protect etcd with TLS, Firewall and Encryption

- Turn on encryption at rest for etcd secrets

- Disable anonymous access with --anonymous-auth=false so that unauthenticated requests get an error response. To do this, the API server needs to identify itself to the kubelet. This can be set by adding the flags -kubelet-clientcertificate and --kubelet-client-key.

-  Isolate Kubernetes Nodes

-  Monitor Network Traffic to Limit Communications

- Use Process Whitelisting

- keeping k8 version up to date

- The kubelet is an agent running on each node, which interacts with container runtime to launch pods and report metrics for nodes and pods. Each kubelet in the cluster exposes an API, which you can use to start and stop pods, and perform other operations. If an unauthorized user gains access to this API (on any node) and can run code on the cluster, they can compromise the entire cluster

- Additionally, encrypting network traffic using technologies like Virtual Private Networks (VPNs) or Secure Socket Layer (SSL) can protect data in transit. Deploying container firewalls within the Kubernetes environment provides another layer of protection.

- Network Segmentation
Namespaces: Use namespaces to isolate different applications and teams within your Kubernetes cluster.

- Network Policies: Define granular network policies to control traffic flow between pods, services, and external networks.

- Pod Security Policies (PSPs)
Restrict Pod Capabilities: Use PSPs to limit the capabilities and privileges of pods, preventing unauthorized actions.
Enforce Security Context: Specify security contexts for pods, including user IDs, group IDs, and SELinux labels.

- Image Scanning and Vulnerability Management
Scan Images: Regularly scan container images for vulnerabilities using tools like Clair, Trivy, or Anchore.
Patch Vulnerabilities: Update images with patched versions to address identified vulnerabilities.

- Secret Management
Kubernetes Secrets: Use Kubernetes secrets to store sensitive information like passwords, API keys, and certificates.
Secret Rotation: Regularly rotate secrets to prevent unauthorized access.

- Admission Controllers
Validate Requests: Use admission controllers to validate incoming API requests, ensuring they adhere to security policies.
Enforce Policies: Implement admission controllers to enforce policies like PSPs and network policies.


- Regular Security Audits and Penetration Testing
Identify Vulnerabilities: Conduct regular security audits and penetration tests to identify potential vulnerabilities.
Remediate Issues: Address any identified vulnerabilities promptly.

- Logging and Monitoring
Monitor Activity: Log and monitor pod, container, and network activity for suspicious behavior.
Alerting: Set up alerts to notify administrators of potential security threats.

- Cluster Hardening
Disable Unused Features: Disable unnecessary features or components to reduce the attack surface.
Secure API Server: Protect the Kubernetes API server with appropriate authentication, authorization, and encryption.

- Regular Updates and Patches
Stay Updated: Keep your Kubernetes distribution, components, and container images up-to-date with the latest security patches.

- Consider Additional Security Measures
Security Context Constraints (SCCs): Use SCCs for more granular control over pod security.

- Network Segmentation with Istio: Leverage Istio for advanced network control and security.

- Container Runtime Security: Implement container runtime security measures like cgroups, SELinux, and AppArmor.


**Metrics to look for, while monitoring the frontend layer**

- Bounce Rates: Correlate slow load times with bounce rates to understand how performance affects user engagement.

- Conversion Rates: Analyze the relationship between frontend improvements and changes in conversion rates.

- Revenue: Connect frontend performance with revenue fluctuations to assess the financial impact of user experience.

- User Engagement: Link performance enhancements to user engagement metrics, such as time spent on site and interactions per session.

- User Journey: Map frontend performance to different user journey stages to identify critical touchpoints.

**Key metrics to monitor**

- Page Load Times: Measure the speed at which your pages load to ensure optimal user experiences.

- Responsiveness: Assess how swiftly user interactions are processed and displayed.

- Error Rates: Keep an eye on errors that might disrupt user journeys.
User Interactions: Analyze how users engage with your application’s features and functionalities.

- Conversion Funnel: Track the progression of users through key conversion steps.

- Third-Party Integrations: Monitor the performance of integrated services or scripts.

- Device Compatibility: Ensure consistent performance across various devices and screen sizes.

**metrics to track the application performance**

- Requests per second

- Data I/O

- Average response time rate

- Peak response time

- Hardware utilization

- Thread count

- Disk usage

- Load

- Network bandwidth

**Metrics related to database performance**

- Deadlocks

- Lock timeouts

- Number of delayed writes and for how long they were waiting
How often the data is spilled to disk

- Length of the transaction log

- Data distribution and how much data we store

- How many nulls we have

- Slow queries

- Number of errors and warnings

- Number of scheduled tasks (vacuuming, index updates)

- Backups and other periodic tasks
