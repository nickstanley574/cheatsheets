# SE441: Continuous Delivery and DevOps Lecture Notes

**Winter 2018 - 2019**

**Prof. Christopher Jones**


## Introduction

A IDC Analyst showed that on average **80%** of system outages are caused by operator or application errors. Everything else days empathizes speed: agile development, business agility etc. Speed might be a goal but it's an outcome! You don't get fast by just going fast. Greyhournd know how to run but it takes training to get them to RUN month and month of ward works. 

### The Myth of Technical Excellence
The Myth of Technical Excellence - whenever we have really hard problems to solve we tend to look for tech-based solutions. THIS IS VERY WRONG! Good Tech is necessary but not sufficient, Software is a **human endeavor** and its useless if there aren't good process to support them, which means CD is about Tech and PEOPLE. We don't solve tech problems we solve people problems. 

Constant incremental improvements typically lead to greater gains than leader, periodic leaps. We are looking at evolving our processes, practices, and people rather than revolutionizing them. 

Software development is essentially a series of experiments. What we delivery (VALUE) and how we deliver it (PROCESS). 

New Technology and tools DO NOT fix a culture, person, or process problem. Comparatively speaking, computers are easy, people are harder. The human factors trumps everything, without voluntary adoption, people find ways to subvert tech. In fairness, there are a lot of problems that can be solved with good tech tooling, but the adoption of too many techs can lead to integration and process problems. 

If CD is the goal we need to emphasizes: 
1. Building Quality in. (We can't compromise quality for speed)
2. Working in small batches
3. Let the computer do the repetitive work and let people solve problems. (Thats more fun anyway)
4. Relentlessly pursue continuous improvement. 
5. Everyone is responsible. 

In time of you focus on these 5 items you will BECOME fast. 

Too often the content of software is thought to be code, the content is business value code is just the mean of delivering that value. Reliably identification and prioritization of values is CRITICAL **(IF YOU CAN'T DO THIS YOU WILL FAIL)**. If you're building the wrong things, fast deploys only ensure that you ship the wrong things faster. (Not a great ROI story) 

Big bang changes can cause distractions. It isn’t that code is leaking out, but business value resulting in unplanned work. For example:
1. Development or testing churn. 
2. Downtime (planned or unplanned) 
3. Let the computer do the repetitive work and let people SOLVE PROBLEMS 
4. Relentlessly purse continuous improvement 
5. Everyone is responsible 

Small batches allowed delivering constant flow of business value.

Doing CD require organizational change! 

Need to balance tech with people; neither one alone guarantee success. 

### Software Economics

All for-profit businesses have the same basic goal – to make money. 

Simple ways to measure ROI:
- Saving by reducing the amount  of unplanned work 
- Saving by reducing outages from bad releases
- Values of activities enabled by the first two options. 

```
cost_of_excess_rework = tech_staff_size * 
                        average_salary * 
                        benefits_multiplier *
                        percent_of_time_on_rework

cost_of_downtime      = deploy_frequency *
                        change_failure_rate (%) *
                        mean_time_to_recover *
                        hourly_outage_cost
```

### Continuous Delivery and DevOps 

Development is also the “experts” when it comes to how its application functions and what it requires to operate successfully. Operations is responsible for the runtime operation and environments of the delivered software.

DevOps promotes a set of processes and methods for thinking about communication and collaboration between development, QA, and IT operations.

According to Martin Fowler, you're doing CD when: 
1. Software is deployable at any time 
2. Deployability is more important than new features 
3. Fast, automated feedback on the prod readiness of all system on any change.
4. On-demand push-button deployments, any version, and environment. 

The Goal is to have low cycle-time (plan -> code -> build -> test -> release -> deploy -> operate -> monitor -> repeat), and high quality releases. 

DevOps Principles: 
1. Every Change leads to a potential release. 
2. Must have repeatable, reliable process for software releases.
3. Automate almost everything. 
4. Keep everything in version control.
5. If it hurts, do it often and bring the pain forward. 
6. Build quality in. 
7. Done means released.
8. Everyone is responsible for the delivery process. 
9. Continues improvement 

### Risks and Rewards 

Release should be Repeatable, Reliable, and Predictable. 

Not developing in prod-like environments can lead to: (1) Inconsistencies in hardware configs (2)  Inconsistent behavior between lower, test and higher, prod envs. (3)  An inability to test hardware and software configs before they are introduced into higher-envs.   

**No one cares if it works on your machine.** Higher environments may be the first time the operations team has
seen the release. All installers, assemblies, configurations, etc. have only been tested in environments that are nothing like production. Different cluster members have different versions of OS, patches, middleware, libraries, etc. **We need to treat configuration like code.**

**One technique: frequent releases!**
- Rewards: 
    - The more frequent the release, the less change is needed.
    - Rollbacks are less risky.	
    - Feedback is faster.
    - Value is realized more quickly.
- Risk: Cost of bugs getting into production.
    - Assumptions: 
        - We know what our customers want. 
        - Bugs are expensive.
        - Testing takes a long time. 
        - All bugs can be found in test.
- Risk: New releases will annoy users.
    - Assumptions: 
        - Releases incur downtime.
	    - Users will notice changes.
	    - Changes are visible to all users.
- Risk: Cost of release is greater than its value.
    - Assumptions: 
        - High coordination overhead. 
        - Releases are risky.
        - Deployment is time consuming.

**Contrary to conventional wisdom, we need to embrace failure – it’s not only always an option, it’s inevitable. WE need to Learn how to fail better! Use cheaper, less reliable hardware. If processes are risky, do them often. Don’t punish people for outages.**

## Theory of Constraints and Value Streams

### Value Stream Mapping 

**Value-stream mapping** is a lean-management method for analyzing the current state and designing a future state for the series of events that take a product or service from its beginning through to the customer with reduced lean wastes as compared to current map.

Value Stream Mapping offers:
- Offers a holistic view of how work moves through a system.
- Maps of material and information flows across the organization.
- Captures value-added work from non-value-added work.

Useful Metrics: 
- **Total lead time (TLT)** - The time needed to complete a process from the time work is ready until that work is complete. 
- **Total Process time (TPT)** - The total time required to actually complete a process. This is typically much less than the TLT. 
- **Process cycle efficiency (PCE)** - `Total process time / total lead time`. The Percentage of the TLT that involves actual work. 
- **Percent complete and accurate (%C&A)** - The percentage of work that each of a processes' downstream consumers considers ready. Anything less Then 100% represents waste.  
- **Rolled  %C&A** -  The overall %C&A for the entire value stream. This is just the %C&A of each process in the value stream multiplied together. 
- **Takt Time** - It's the cycle time ended to keep up with customer demand. Takt time = `available production time per-day / Demand per day`. (IF the Toal lead time is greater then take time the org will not keep up with demand.)

### The Theory of Constraints

**The theory of constraints (TOC)** is a management paradigm that views any manageable system as being limited in achieving more of its goals by a very small number of constraints. There is always at least one constraint, and TOC uses a focusing process to identify the constraint and restructure the rest of the organization around it. TOC adopts the common idiom "a chain is no stronger than its weakest link". This means that processes, organizations, etc., are vulnerable because the weakest person or part can always damage or break them or at least adversely affect the outcome. (**Every value stream or workflow has some constraint in it  and unless you deal with it in some fashion any other place you optimize doesn’t matter.**)

Simple/basic premises: 
1. Every system is constrained in some way
2. Any changes to the system that do not improve throughput at the constraint cannot improve the throughput of the overall system.

## The Three Ways

### 1. The Principles of FLOW: 

- Make work visible
    - Use visual management.    
    - Avoid trigger work from emails and chats - all work should flow through the same process of prioritization.
    - Make sure that each work center has its own queue of work.
    - Use these work boards to capture important metrics
- Limit Work in Progress (WIP)
    - People are horrible and multitasking (THIS IS FACT) 
    - Limit the number of concurrent tasks
    - Wait times need to be managed. `wait_time = % Resource is Busy / % Resource is idle`
- Reduce batch sizes
    - We want to deliver value as rapidly as possible.
- Reduce the number of handoffs
    - Information is always lost during handoffs.
    - Handoffs require time and effort to setup and coordinate.
- Continually identify and elevate constraints
    - To optimize:
        1. Identify the limiting constraint(s) in the stream.
        2. Exploit the constraint. If the constraint is idle, that value is lost forever.
        3. Subordinate everything to the constraint. This means other resources may be underutilized.
        4. Delays upstream don’t usually average out farther downstream other than by accident.
        5. Elevate the constraint. If cycle time is too long, there is more work to do.
        6. Find the next constraint and repeat the process.
    - Eliminate hardship and waste in the value stream
	    - Extra processes that add no value to the customer.
	    - Extra features that don’t meet either business or customer needs.
	    - Task switching.
	    - Heroics (DON'T BE A HERO YOU ARE NOT SUPERMAN YOU WILL HATE YOU LIFE ... Process > Heros) 

### 2. The Principles of FEEDBACK

Problems need to be visible. Feedback and feed forward loops can help address this. 

Prevents problems from moving downstream – easier and cheaper to fix them close to the point of origination.

Adding more steps to a process often makes that process even less reliable because it can lead to significant deviations between who should do a certain task who actually does that task. (Example Most documentation.) 

### 3. The Principles of CONTINUAL LEARNING AND EXPERIMENTATION. 

Common organizational cultures:
- **Pathological** - Large amounts of fear and threat. Information is hoarded or used for political gain. Failure is hidden. (RUN AWAY) 
- **Bureaucratic** - Governed by rules and processes. Teams defend their own area of responsibility. Failure works through some form of judgement. (Depends on the business demands can be good often is not needed) 
- **Generative** - Actively seeks and shares information. Responsibilities are shared across the value stream. Failure is reflected and improved upon. (This is the goal) 

If processes are not actively improved, they’ll degrade over time. 

Do not shy away from disruptions or failure. Become resilient by learning how to react too and recover from inevitable problems. Make opportunities to experiment and try new things so that you know where the failure points are in your organization and systems and how to deal with them.

Leaders encourage their people to embrace learning. Encourage employee experimentation by asking questions.

## Source Code Management and GIT

**Configuration Management** refer to the process by which all artifacts relevant to your project, and the relationships between them, are stored, retrieved uniquely identified and modified. 

Source code management tools, often referred to as “version control”, are the best way to manage source code and related assets. Concurrent, consistency, history and recoverability. 

Good configuration management provides benefits: Any environment including its OS, patch level, network configuration, software stack, applications, and application configuration can be reproduced on demand. Incremental changes to any of the above can be easily made and deployed across environments. Changes to each environment can be traced to find out when the
change was made, who made it, and why. **All compliance regulations and requirements are satisfied.**

- **Concurrent Modification Model:** Work is easily lost. He who saves last wins.
- **Lock-Modify-Unlock:** No concurrent development on shared files. Developers frequently forget to unlock their files.
- **Copy-Modify-Merge:** Allows concurrency. Merges can be painful.

**Version control is the single most important tool in the DevOps and continuous delivery space.**

### Git Basics

Earlier SCMs managed changes by tracking the deltas from one version to the next. Git stores the entire file rather than the deltas. Requires more disk, but disk is NOW MUCH cheaper compared to developer time. Linus Torvalds, father of Linux, wanted an SCM that could keep up with the Linux contributor community.

A repository holds everything under Git’s control for a particular project. It contains a complete history of all of the resources and activities that have ever been part of the project.
- **Blobs (Binary large objects)** store the actual data about each file within the repository. Every object in the repository is given a SHA1 hash. This hash allows git to detect changes to the blob.
- **Trees** store the metadata about blobs including: Identifiers Pathnames and Links to other trees.
- **Commits** store the metadata about shareable changes including: Committer, Commit date, Log message, A link to a tree representing the state of the repository. 
- **Tags** store the metadata including: Tag name, Commit identifier.

### Branching Models and Feature Flags 

**Branching models significantly impact release rate.**

Centralized workflow:
- Branches are created for each change or feature
- Branches are pushed to the central server and a pull request is created.
- The change is reviewed before being merged into the Master branch.

“Gitflow” workflow:
- Master represents production-ready code. Branched to Develop and Hotfix.
- Hotfix represents emergency changes. Merged to Master and Develop.
- Develop represents latest delivered changes for next release. Branched to Feature branches. Merged to Release.
- Release represents a staging area for the next release.
- Feature branches contain individual changes or features. Always merged back to Develop.

Merges are evil. In the best case we could avoid them. One such approach is called **trunk-based** or **mainline development**. 
- Each merge is cherry-picked – we don’t try to bring every change into the release; only the most important ones.
- One branch is created for each release.
- Developers can only commit to the trunk, not to the release branch.
- Release engineers create the branches and cherry-pick individual commits from the trunk into them.
- Developers should not break the build with any commit.
- Merges back to trunk are few and far between – only if an issue cannot be reproduced in the trunk itself.
- If all commits are done against trunk, how do we handle new features? We need a way to disable features until they’re ready to be released. he answer is a technique called **feature flags** or **feature toggles**. 

### Software Configuration

- Too much time spent in designing configurations (which need to be tested) rather than solving the actual problem.
- Configurations usually can’t be tested until run-time.

Configuration can be injected at: Build time, Packaging time, Deployment time, Run time

We often need an application’s configuration to vary at different levels of granularity: Environment, Data Center, Tier, Server. **This can lead to configuration file “bloat” where many different configuration files need to be managed.** 

## Build Automation 

Automation Benefits: 
- **Repeatability**: The build will always follow the same sequence of steps and generate the same outputs. 
- **Consistency**: The steps executed during the build will be the same regardless of the person executing the build. 
- **Portability**: The build process is tried to the product and not to any particular developer's machines or environment.
- **Integration**: The build can be executed as part of an automated CI process.    

Java Automation tools: 

| Tool  | Code      | Style                     | Lifecycle |
| ---   | ---       | ---                       | ---       |   
| Ant   | XML       | Imperative                | None      |
| Maven | XML       | Declarative               | Depends on artifact type and applied plugins |
| Gradle| Groovy DSL| Imperative & Declarative  | Depends on artifact type and applied plugins |

- Ant provides no default lifecycle save the guarantee that it will attempt ,to execute whatever target you specify on the command line or the default target otherwise.
- Maven’s default lifecycle provides for things like compilation, testing, and packaging. The lifecycle will change based on the kind of artifact being built.
- Gradle’s lifecycle is more complex:
    - **Initialization**: Gradle determines what projects will participate in the build.
    - **Configuration**: Gradle determines what takes will be performed and defines the DAG (directed acyclic graph) by which they will be executed. 
    - **Execution**: The tasks in the DAG are actually performed.

### Dependency and Artifact Management

Software artifacts generally do not work in isolation. They usually depend on other software artifacts. The process of maintaining the various artifacts that support our applications is called **dependency management**.

Dependency management can be one of two types:
- **manual**: A developer is responsible for downloading all of the required dependencies as well as their dependencies. (Can require a significant time investment. Increased risk of error.)
- **automated**: In an automated approach, the dependencies of an artifact are declared. (Time investment can be less. Ris of error is reduced.) 

Best Practices:
- Version numbers in the file name.
- Manage transitive dependencies
- Resolve version conflicts

The `groupId`, `artifactId`, and `version` comprise the artifact’s coordinates. 

**Ant + Ivy (build.xml)**

Ant by itself doesn’t provide any form of dependency management. For that we need to use Ivy. Ivy can use all Maven repositories.

- `ivy:resolve`. Calculate the dependencies and download them to the local Ivy cache.
- `ivy:install`. Installs modules from an public repository into an enterprise repository.
- `ivy:retrieve`. Retrieves all artifacts into a local directory.
- `ivy:publish`. Publishes new artifacts to the enterprise repository.

**Maven (pom.xml)**

Maven recognizes six (6) different scopes, but we only care about the following four (4):
- `compile`. The dependency appears on all classpaths.
- `test`. The dependency appears on the test classpath.
- `runtime`. The dependency appears on the runtime classpath.
- `provided`. The dependency appears on the compile and test classpaths.

**Gradle (build.gradle)** 

Gradle uses the same dependency resolution process as Maven by default.

In a nutshell, the process is as follows:
1. Look for the artifact in the local cache. If it’s there, add that path to the classpath.
2. If it isn’t in the local cache, start looking at each remote repository that the Maven project knows about.
3. Look for the artifact in the remote repository. If it’s there, download it into the local cache and add that path to the classpath.
4. If it wasn’t found in the remote repository, proceed to the next remote repository and check again. Keep checking until we either run out of repositories or until we successfully find and download the artifact.

The fact that we can download artifacts from the internet provides both opportunities and challenges:
**Pros:** Convenient, Inherent redundancy, Standard practice.  
**Cons:** Variability in controls, Relies on goodwill and No way to prevent downloads
We can use an artifact repository to help mitigate the risks of using automate dependency management.

An **artifact repository** is software that intermediates between your build scripts and the internet. They typically provide Repository proxying, Artifact caching, Artifact blacklisting and Security and auditing. It becomes a time machine that contains a complete history of your deployable artifacts.

(Midterm)

### Continuous Integration

The sequence of activities that each change triggers is what constitutes an application’s **build pipeline**.

CI requires: 
1. Source Code Control 
2. Automated Tests suites
3. Short build processes
4. Managed development workspaces. 

**Best Practices:** 
1. Don't commit on a broken build.
2. Run all tests locally before committing. 
3. Wait for commit tests to complete. 
4. Never go home on a broken build. 
5. Always be prepared to revert to the prior version. 
6. Tome-box fixing before reverting.
7. Don't comment out failed tests (yes really this is a issue)
8. You are responsible for anything that breaks b/c of oyu changes. 
9. Test-driven development. 

### Deployment Pipelines 

#### Stages 
* **commit:** checkout latest, compile, static code analysis, unit tests, prepare artifacts for downstream stages. 
    * Wait until the current commit stage of the pipeline succeeds before kicking off a new one. 
* **Acceptance Tests:** Execute automated functional and non-functional tests.  
    * Run the tests ina scaled down version of prod
    * Make sure all major components are present 
    * Tests are owned by the entire team abd build be everyone 
* **User Acceptance Tests:** Exploratory, New Feature and Usability Testing 
    * Avoid regression testing
    * Focus on thing that are difficult to automate. 
* **Capacity:** Determine if the application can run under a sustained load. 
    * Design automated tests
    * Dynamically provision testing env. 
* **Production:** Getting the app installed into the prod runtime env. 
    * Automate the deployment process. The same process should be used across all envs. 
    * Automate a smoke test to verify the installation
    * Devise and test a rollback plan. 

**Best Practices:** 
1. Only Build binaries once
2. Deploy the same way to each env. 
3. Smoke test the deploy 
4. Deploy to Prod-like envs
5. Each change should flow through the pipeline immediately.
6. If any part of the pipeline fails, stop everything until it's fixed. 

Pipelines can provide metrics that may help us improve the process: 
* Test Coverage. 
* Defect density. 
* Velocity. 
* Number of commits, builds, failures per day.
* Duration of stages. 

## Infrastructure, Virtualization, and Cloud Computing

### Infrastructure

An environment is all of the resources that your application needs to work and their configurations. 
- The OS and its configuration.
- All middleware and its configuration.
- All infrastructural software (e.g. version control, monitoring, etc.) and its configuration.
- All external integration points.
- All network infrastructure (e.g. routers, DNS, firewalls, etc.) and its configuration.
- The relationship between the development and infrastructure teams.

Guiding principles: 
- Specified through version-controlled configuration.
- Autonomic, automatically correcting itself to the desired state.
- Observable through instrumentation and monitoring.

Operations has different needs from development (stability vs. delivery):
- Change management process. 
- Automated monitoring and alerting.
- Continuity planning and disaster recovery.
- Deployment and release processes.

When making change to infrastructure:
- Every change should go through the same change management process.
- The change management process should use a single ticketing system that can provide useful metrics.
- The exact change should be logged so it can be audited later if necessary.
- It should be possible to see a history of all changes, including deployments.
- The change should have been tested in a production-like environment before being made to the actual production environment.
- The change should be made to version control and then applied using the automated tools.
- There should be automated tests to confirm that the change worked as expected.

### Virtualization 
Platform virtualization means simulating an entire computer system so as to run multiple instances of operating systems simultaneously on a single physical machine.

**Type 1 & 2 Virtualization:** The material describes a Type 1 hypervisor as running directly on the hardware with VM resources provided by the hypervisor. The IBM Systems Software Information Center material further states that a Type 2 hypervisor runs on a host operating system to provide virtualization services.

Benefits: 
- Consolidation.
- Standardizing hardware.
- Easier-to-maintain baselines images.
- Easier to simulate abnormal system conditions.

### Cloud Computing 
There are three types of clouds:
1. **Public.** Managed by a provider but open for use by the public
2. **Private.** Virtualizes and shares the IT infrastructure within a single organization.
3. **Hybrid.** A mixture of both public and private.

Key enablers of clouds include: 
- Extremely large-scale, commodity-computer datacenters.
- Low-cost locations.
- Decreases in the cost of energy, operations, software, and hardware by factors of 500-700%.
- The ubiquitousness of large-scale computing across industry verticals.
- The ability for providers to make a profit.

Use a cloud when: 
- Demand for services varies by time (e.g. Cyber-Monday demand vs. normal demand).
- Demand is unknown (e.g. startup companies).
- Demand that can leverage significant parallelism (e.g. batch computing that can use 1000 machines for 1 hours vs. 1 machine for 1000 hours).

All applications require some key elements: **computation**, **storage**, and **connectivity**.

**Elasticity** is about adding or removing resources as the needs of the applications change. Elasticity is all about pay-as-you go pricing.

#### Cloud Obstacles

Technical obstacles to cloud adoption:
- Perceived (un)availability of a service.
- Data lock-in (e.g. how to retrieve data and applications).
- Data confidentiality and auditability.

Business obstacles to cloud adoption: 
- Reputation fate sharing.
- Software licensing.

Technical obstacles to cloud growth: 
- Data transfer bottlenecks.
- Performance unpredictability.
- Scalable storage.
- Bugs in large-scale distributed systems.
- Scaling quickly.


###  12 Factor Applications

The Twelve-Factor App is a set of guidelines for building software-as-a-service.

1. **One codebase tracked in revision control, many deploys.**
	- If there are multiple codebases, it’s not an app – it’s a distributed system.
	- Multiple apps sharing the same code is a violation of twelve-factor. 
2. **Explicitly declare and isolate dependencies.**
	- Never rely on the existence of system-wide packages.
	- Avoid calling out to external packages. 
3. **Store config in the environment.**
	- Use environment variables for all configuration.
	- Can’t be checked accidentally (or deliberately) into source code control.
4. **Treat backing services as attached resources.**
5. Strictly separate build and run stages.
	- The build stage is a transform which converts a code repo into an executable bundle known as a build.
	- The release stage takes the build combines it with the deploy’s current config.
	- The run stage runs the release in the execution environment
6. **Execute the app as one or more stateless processes.**
	- Never use sticky sessions.
	- Ensures that applications can easily be started, stopped, or relocated without loss of critical, transactional data.
7. **Export services via port binding.**
	- The app is completely self-contained and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service.
8. **Scale out via the process model.**
9. **Maximize robustness with fast startup and graceful shutdown.**
	- Processes are disposable, meaning they can be started or stopped at a moment’s notice.
10. **Keep development, staging, and production as similar as possible.**
11. **Treat logs as event streams.**
	-  The streams will ideally be sent to a log aggregator for further analysis and querying.
12. **Run admin/management tasks as one-off processes.**


## Above the Clouds: Berkeley View of Cloud Computing (Supplemental Reading) + Worksheet 

### Problem 1: 
A service has a predictable daily demand where the **peak** requires **250 servers**, but the **trough** requires only **50 servers**. On **average**, we need **150 servers** per day. Each server hours costs **$5.00/hr in a datacenter** and **$4.20/hr with a cloud provider**.
```
pek_num_servers         = 250 
tro_num_servers         = 50
avg_num_servers         = 150 
server_hr_usage         = 24
cloud_compute_cost_hr   = $4.20
datac_compute_cost_hr   = $5.00
```
1. How many server hours per day do we actually need? 
```
avg_num_server  * server_hr_usage   = avg_total_server_hours 
150             * 25                = 3,600 hrs/day
```
2. How many server hours per day must we actually provision? (HINT: you need enough server for PEAK usage)
```
pek_num_servers  * server_hr_usage   = pek_total_server_hours 
250              * 24                = 6,000 hrs/day  
```
3. What is the annual cost difference between hosting the application in our own datacenter versus hosting with the cloud provider?
```
hosting_in_cloud_yr    = avg_total_server_hours * days/yr * cloud_compute_cost_hr
                       = 3,600                  * 365     * $4.20 
                       = $5,518,800 

hosting_datacenter_yr  = pek_num_servers        * days/yr * datac_compute_cost_hr
                       = 6,000                  * 365     * $5.00
                       = $10,9500,00

annual_cost_diff       = hosting_datacenter_yr - hosting_in_cloud_yr
                       = $10,9500,00          - $5,518,800 
                       = $5,431,200 
```
### Problem 2: 
Suppose we create **250 GB** of new data each week that needs to be analyzed and we have **8 local servers** for that processing. A computer the speed of **one EC2 instance takes 2 hours per GB** to process the new data. (Assume that 1GB = 10**3 MB). 
```
new_data            = 250 
num_local_server    = 8 
server_speed_hr     = 2 GB/hr 
```
1. How long will it take us to process each week's data locally? 
```
local_proc_speed_hr = new_data * server_speed_hr / num_local_server 
                    = 250      * 2               / 8 
                    = 250      * 0.25 GB/hr 
                    = 62.5 hrs
```     
2. How much would it cost to process the data locally assuming each server hour costs **$4.50**?
```
local_compute_cost_hr = $4.50

local_proc_cost = num_local_server * local_proc_speed_hr * local_compute_cost_hr
                = 8                * 62.5                * 4.50
                = $2,250
```
3. How many cloud compute instance would we need to complete the analysis in one hour? 
```
num_ec2_1hr = new_data * server_speed_hr 
            = 250 * 2
            = 500 
```
4. How much does the computation cost to process the data with our cloud provider assuming that each server hour of compute time costs **$0.075**?
```
cloud_compute_cost_hr = $0.075

cloud_data_compute_cost = num_ec2_1hr * cloud_compute_cost_hr
                        = 500         * $0.075
                        = $37.50 

```
5. What is the transfer cost to move the data to the cloud provider assuming that each GB will cost **$0.10** to transfer? 
```
data_transfer_cost_gb = 0.10/GB

total_transfer_cost   = new_data * data_transfer_cost_gb
                      = 250 * 0.10
                      = $25
```
6. How long will it take to transfer the full 250 GB of data to the cloud provider assuming that they can sustain an avg of **20 Mbits/sec**?
```
transfer_speed_mbits_sec = 20 Mbits/sec 

total_transfer_time = (new_data * 1000mb * 8bites) / transfer_speed_mbits_sec
                    = (250      * 1000mb * 8bites) / 20 
                    = 20,000,000 / 20 
                    = 100,000 sec / 3600 (sec/hr) 
                    = 27.8 hrs
```
7. How much will it cost to process one week's data in the cloud? 
```
total_cloud_cost = cloud_data_compute_cost + total_transfer_cost
                 = $37.50                      +  $25 
                 = $62.50
```
8. Compare the processing time and overall cost. 

|      | Local    | Cloud    |
|------|----------|----------|
| Cost | $2,250   | $62.50   |
| Time | 62.5 hrs | 27.8 hrs |




## Automating Infrastructure

Once servers have been provisioned, they should never be changed in uncontrolled ways. This means: No one should have access to any of the boxes except for the operations team. Any change should be automated and preferably stored in your source code control system.

### Vagrant
- All Vagrant VMs are based off of `boxes`; images from which VMs can be built.
- Boxes are installed from images in Vagrant’s external repository, called the `box catalog`.
- The `base box` is the image that we’re going to use as the basis for our future customizations.
- `Providers` represent the runtime environment in which our virtual machines will be executed.
- `Provisioners` are the methods we will use to make our custom changes to the base image resulting in the final image that we’ll execute.
- All instructions for the creation of a VM are embedded in a `Vagrantfile`.


### Chef
- `Configuration Management Tool`: These tools often define a DSL (domain-specific language) that abstracts away the complexity of configuring a system.
- Chef is resource-based. Declarations assert resources and their state, not how that state will be achieved.
- Chef `cookbooks` are used to manage `recipes`.
	- Cookbooks make it easier to organize the contents of one or more recipse.
	- A cookbook is intended to exhibit the single responsibility principle.
	- Chef recipes are collections of related resources that describe a particular configuration.

### Terraform 
Software for automating the creation and provisioning of cloud based resources.

## Containerization and Docker

### Containerization
- Allows for true "build once, run anywhere." 
- Each container is effectively sandboxed.
- Allows for container-based promotions across envs.
- Platform compatibility becomes less of an issue.
- Supports separation of responsibilities between dev and ops.  
- Strong support for CD since containers are much more lightweight than VMs. 

Conceptually containers can be thought of as **“lightweight VMs”**. However, they share all of the resources of the host OS – there is no guest OS. A container is just a process running under control of the computer’s main OS.


### Docker Overview 

Images are read-only templates that contain everything that the container needs in order to fulfill its purpose. Docker images are composed of “layers” that are combined into a single image via a Union File System  Similar to artifact repositories, but hold Docker images. Registries can be private or public. 

#### Docker Images 
- Every Docker image begins with a `base image`. Any available image can be a base image.
- Additional instructions are used to add layers to the base image. 
- Instructions are declared in a text file called a `Dockerfile`.
- The `docker images` command lists images.
- The `docker pull` command downloads an image.
- The `docker history` command lists the various image layers.
- The `docker rmi` command allows you to remove an image.

#### Docker Containers (steps)
1. Retrieve or download the image
2. Create the container
3. Allocate a filesystem and mount a read-write layer
4. Allocate a network/bridge interface.
5. Setup and IP address
6. Execute the specified process.
7. Capture and stream application output.

#### Dockerfiles
- `Dockerfile` - a file of instructions. These instructions are applied to a base image to create a new image that can then be made available to other people through a repository.
- `RUN` - instruction performs a task. It’s generally used for things like installing software, creating directories, or setting environment variables. Each `RUN` results in a new layer.
- `ADD` - instruction copies an archive file from the host and unpacks it in the image.
- `COPY` - instruction is like an `ADD` except that it doesn’t extract the contents of the file – it’s moved as is.
- `EXPOSE` - instruction defines which ports the image will make available for port mapping.
- `VOLUME` - instruction defines volumes within the container to which we will attach hosted directories when we run the container.
- `ENTRYPOINT` - instruction defines the executable that will be invoked when the container is started.
- `CMD` - either acts as a replacement for the `ENTRYPOINT` or adds it’s parameters to those provided to the `ENTRYPOINT` on container startup.

#### Docker-Compose
Docker-Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a `YAML` file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. Docker compose will create a virtual network on the host. Each service will be added to that network as a host, with the service’s name becoming the DNS name of that service within that virtual network.

#### Kubernetes
- Kubernetes is used for container orchestration. This provides for more efficient use of VMs that are hosting docker containers well as fault tolerance and recovery.
- Kubernetes works within a cluster of computers called nodes, which are the workers that actually run applications.
- Applications in Docker containers are deployed to pods, which represents a group of containers and any shared resources they require.

## Operations, Databases, and Testing

### Operationalization

Compliance and auditing usually have some common requirements:
- Effective change management processes.
- Appropriate and understandable documentation of all processes (e.g. for independent auditors, not you).
- Authorization barriers (e.g. the same people who write the software are not also able to deploy it).
- Approvals for deployment.
- Deployment auditing and traceability

Auditors often want documentation of key processes. They will not always accept that the automated version of that process suffices. 

Authorization barriers are all about separation of concerns.

**Change management** is the process by which changes are introduced into a production environment.

### Operations

**Logging** is concerned with capturing diagnostic information about an application’s behavior. Get your logs off the individual machines and into a log processing syste If you need to log into a server to look at your logs, then you’re doing something seriously wrong. 

**Monitoring** is concerned with determining if your application or its environment is behaving as expected.

**Disaster recovery** is the process of returning your applications to service after a major incident that brings down one or more key components of the application stack

### Database Management

Database changes are different from other application changes because:

Database changes are different from other application changes because:
- The database is a shared resource.
- Updates are more complex than simply updating files on disk and can take a long time to complete.
- Unless explicitly planned for, changes will not be backwards compatible, making rollbacks challenging.

Parallel Change Pattern or expand-modify-contract pattern.
- In phase 1 we provide access to the new version of the database.
- In phase 2, applications are gradually changed to take advantage of the new schema.
- In phase 3 the old schema is torn down.

The idea here is simple – the currently deployed version of the application is always compatible with both the current and future database state. This means a new version of the application might be released that is able to use a version of the database that doesn’t exist in production yet.

**Testing DBs:** Test data is needed for both manual and automated tests. The general approach is that a test creates its test data during a setup step and destroys it during the teardown step. Using an in-memory implementation makes clean-up simple – the instance is simply shutdown and destroyed and a new instance created when the tests need to run again. You might not do this beyond unit testing since we want to use the same database in the QA environment as we use in the PROD environments.


### Testing and Code Quality Analysis

Unit tests answer questions like:  
- Developers: “Does my code work as I expect?”, 
- Developers: “Have my changes introduced a defect?”

Acceptance tests answer questions like: 
- Developers: “Am I done?”, 
- Users: “Did I get what I wanted?”

Exploratory and usability tests answer questions like:
- Users: “Is there any unexpected behavior?”, 
- Users: “Is the application fit for use?”

Performance, security, and monitoring tests answer questions like:
- Developers: “Will the application scale?” 
- Users: “Is the application responsive?”
- Developers: “Is the application secure?”
- Users: “Is my data safe?”
- Developers: “Will I know if the application goes down?”
- Users: “Will they know if the application goes down?"

**Automating Acceptance Tests with BDD** - In behavior-driven development features, called stories, are described in the given-when-then.
1. Given: Some conditions...
2. When: A stimulus is applied...
3. Then: Certain conditions should be met.

**Automated Tests:**

| Pros                                                                      | Cons                              |
|---------------------------------------------------------------------------|-----------------------------------|
| Faster feedback.                                                          | Expensive to build and maintain.  |
| Reduced tester workload and Allow testers to focus on higher-value tasks. | May require specialized tools.    |
| Act as a regression test suite.                                           | Needs to be rolled out carefully. |
| Can act as requirements documents.                                        | Difficult to test UIs.            |

If our application depends on lots of other moving parts, this can make the test environment very difficult to manage, maintain, and evolve.

Test doubles allow us to control the behavior and perform better testing:
- **Dummy** objects just satisfy argument lists.
- **Fake** objects have actual implementations, but are not suited to production.
- **Stubs** return pre-fabricated answers to requests.
- **Spies** are stubs that record information about the calls that were made to it.
- **Mocks** are configured with expectations that define the expected interaction with the object.

 
