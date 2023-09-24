# Food Remedy - GCP Infrastructure Proposal

The purpose of this document is to summarise and propose cloud
infrastructure solutions for Food Remedy on Google Cloud Platform (GCP).

## Application Runtime Environment and Infrastructure

The Food Remedy application is planned to run in Docker containers,
which provide a lightweight execution environment without the burden of
managing more complicated virtual machines. These are designed to be
platform-independent and can ensure a level of similarity between each
engineer's development environment and the production environment.

When designing a solution around containers, it's important to consider
that containers by nature should be ephemeral (they might be created or
destroyed at any time) and immutable (they should be built from a
Dockerfile with everything they need to run, and not changed at
runtime).

GCP offers three services for running applications in containers.

| Service                        	| Summary                                                                         	| Pros                                                                                                                                                                                                       	| Cons                                                                                                                                                                           	|
|--------------------------------	|---------------------------------------------------------------------------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Google Kubernetes Engine (GKE) 	| Fully managed Kubernetes cluster                                                	| - Fully managed by GCP, no servers to  maintain. Once set up with Kubernetes manifest templates, should be relatively easy to re-provision environments. Autopilot mode provides simple management options 	| Requires some Kubernetes knowledge  More expensive than other services, especially with autopilot mode.                                                                        	|
| Cloud Run                      	| Run stateless containers as serverless functions, invocable via HTTP requests   	| Pay per use pricing  Good for asynchronous, background tasks                                                                                                                                               	| Requires  architecting application as stateless micro services. More complex for short-term student projects Better for event-driven applications than long-running containers 	|
| Google Compute Engine          	| Lower-level compute platform that supports container-optimised virtual machines 	| Most control over hardware. Can use container-optimzied VM images.                                                                                                                                         	| Must manage VMs which host containers. Must manage server security, networking, hardening, patching etc.                                                                       	|
|                                	|                                                                                 	|                                                                                                                                                                                                            	|                                                                                                                                                                                	|

**Recommendation**: GKE

In addition, GCP provides the **Artefact Registry** service to host
container images. As a fairly simple registry for docker images, there
aren't really any downsides or realistic alternatives for hosting images
on Google Cloud. We could host our own container registry on a server,
but the operational and cost overhead for that would not be worth it for
our simple use case. For each server we run we would need to manage
patching, uptime, networking, hardening and security ourselves. In
addition, GCP's Artefact Registry integrates natively with the GCP
platform. Using this service would also not greatly impact the
platform-independence of our solution, as other major cloud provides
such as AWS and Azure provide similar container registry services with
only small differences in configuration.

The deployment process for our backend will likely involve updating
containers in a registry, with our container orchestrator having logic
to decide how the old containers are stopped and the new containers are
started.

## Database Infrastructure

There are 2 major options for hosting relational databases on Google
Cloud. The **Cloud SQL** service is GCP's native relational database
service for MySQL, PostgreSQL and SQL Server. Alternatively, all major
SQL database engines can run on docker containers and run in our chosen
container runtime (outlined above).

There are pros and cons to each approach.

| GCP Database Option 	| Pros                                                                                                                 	| Cons                                                                                                                                                                                                                                                                                                                                        	|
|---------------------	|----------------------------------------------------------------------------------------------------------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Cloud SQL           	| Security managed by GCP  Patches managed by GCP Data persistence managed by GCP Uptime and reliability managed by us 	| Supports limited number of DB engines (though these are the  most likely ones to chose anyway) Lock in: We are somewhat locked to the Cloud SQL service, however there are reasonable options for migrating between providers of major database engines like MySQL and PostgreSQL                                                           	|
| Docker container    	| Portability  Possibly cheaper                                                                                        	|  We would need to provide our own data persistence as containers are designed to be spun up and down as needed. Additional costs involved in using Compute Engine hard disks.    Security managed by us   Patches managed by us   Uptime, reliability managed by us   More complex - must build and configure suitable containers ourselves 	|

**Recommendation:** Docker Container

Load Balancing

Requests from users in the public internet will need a secure way to
interact with the backend in our cloud. In general, application and
database servers should be hosted in private networks, with requests and
responses going via a load balancer or reverse proxy, which is hosted in
public networks. GCP provides a managed service called **Cloud Load
Balancing,** which is highly scalable and offers application-layer load
balancers. This also allows our app to be available via a single global
IP address which simplifies DNS setup.

The alternative is to run a container with a reverse proxy such as ngrok
to network between the public internet and our backend. As per comments
around running databases in containers, this does leave our project team
with more overhead in terms of managing security, networking, patching
and uptime ourselves. In the case of the Cloud Load Balancing service,
pricing is very cheap especially for a low-volume of requests.

Another critical consideration is protection against DDoS attacks.
Automated attacks can and malicious requests are a serious threat for
even minor applications if they are hosted on the public internet. The
Cloud Load Balancing service can provide automatic protection through
the **Google Cloud Armor service**, whereas running our own load
balancing server would require us to configure this ourselves.

**Recommendation:** We should funnels requests to our backend services
using the Cloud Load Balancing service with Cloud Armor enabled.

Regions and Zones

GCP offers many regions and zones for services to run across the globe.
For Food Remedy, the most relevant will be the *australia-southeast1*
(Sydney) and *australia-southeast2* (Melbourne). All the major services
that are likely to contribute to our solution operate in both regions.
Service pricing for each region is the same. Given this project's
association with the Victorian Government, there may be some compliance
or regulatory issues with data being outside the state of Victoria.

**Recommendation:** Use the *australia-southeast2* (Melbourne) region.

## Security Proposal

As cyber security threats are a common occurrence in society today, we
want to be sure to implement security measures that provide Food Remedy
with protection from unauthorized use and cyber-attacks. Through our
proposal of wanting to use the Google Cloud Platform (GCP) we are
provided with the added security measures already implemented into the
platform. There may be some uncertainty around cloud platforms however
the security measures in GCP are made specifically for GCP, which
provides some reassurance.

If our proposal to use GCP is approved, we would be adopting some of the
security measures already implemented into platform. Some of the
included security features are:

-   Identity and Access Management (IAM)

    -   To ensure the implementation of user privileges which is an
        important cyber security measure, GCP has Identity and Access
        Management which allows for access control and user privileges
        to be set for the cloud infrastructure. Identity and Access
        Management is a security feature that will allows for the
        administrator of Food Remedy to authorise specific access to
        specific users. Not all users will be required to have access to
        all resources so administrators will decide who requires access
        to what resources.

-   Cloud Audit Logs

    -   Often cyber-attacks can occur unnoticed due to logs of activity
        not being kept. Through the use of Cloud Audit Logs, we will be
        able to keep track of any administrative actions and accesses
        that occur. If user permissions are changed, we will have
        records of that, which we can look back on to establish whether
        those actions were legitimately completed by an authorised
        administrator.

-   Virtual Private Cloud (VPC)

    -   Configure the firewall settings to assist in the prevention of
        unauthorized access and data exfiltration.

-   Cloud Amour

    -   Uses technology to detect security issues and potential attacks.
        The protection techniques aim to protect again various threats
        including DDoS and SQL injection. It also incorporates the use
        of Web Application Firewall (WAF) which protections web apps.

Some vulnerabilities of the GCP security measures relate to issues of
misconfiguration and internal threats. To ensure the security measures
work to their best capabilities they must be configured correctly, and
it will be the administrations duty to ensure appropriate configuration.
The risk of internal threats can be managed by using access control and
ensuring the principle of least privilege in implemented allows users
access to the areas and resource they require and not anymore. Regular
review of access control will need to update to ensure privileges are
correct and users no longer requiring access have their privileges
removed.

The security measures provided by GCP allow us to have control of the
security configurations and our cloud infrastructure incorporated all
together, rather than adding external security measures. We are also
guaranteed that the GCP security measures are suitable for cloud as this
is what it was designed for.

## Important Considerations

Cost: What is our budget per month? We must ensure our services fit
within our budget and are unlikely to exceed that budget due to
misconfigurations.

Handovers: Project must be handed over to a new cohort of students each
trimester. Additional complexity will make this more difficult. This is
especially true if server maintenance and patching is involved.

Timeframe: Project length relatively short. Is it worth standing up more
complex services and over-optimising, versus preferring managed services
with limited overhead?

What domain name will Food Remedy use?

## Sources

[[https://cloud.google.com/compute/docs/containers]{.underline}](https://cloud.google.com/compute/docs/containers) -
containers on Compute Engine

GKE Autopilot:
https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview

Artifact Registry:
[[https://cloud.google.com/artifact-registry]{.underline}](https://cloud.google.com/artifact-registry)

Cloud SQL: https://cloud.google.com/sql

GCP Load balancing:
[[https://cloud.google.com/load-balancing]{.underline}](https://cloud.google.com/load-balancing)

GCP Load balancing Cloud Armor:
<https://cloud.google.com/load-balancing/docs/tutorials/faster-performance-improved-protection>
