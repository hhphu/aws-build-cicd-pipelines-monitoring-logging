# Continuous Integration and Continuous Deployment

1. **[Fundamentals of CI/CD](#fundamentals-of-ci/cd)**
2. **[Benefits of CI/CD](#benefits-of-ci/cd)**
3. **[Best Practices](#best-practices)**
4. **[Deployment Strategies](#deployment-strategies)**
5. **[Blue Green Deployment](#blue-green)**
6. **[Key Terms](#key-terms)**

## <a id="fundamentals-of-ci/cd"></a>Fundamentals of CI/CD
### Continuous Integration:
- Practice of merging all developers' working copies to a shared mainline several times a day.
- Include: compiling codes, unit testing, static analysis, dependency vulnerability testing, store artifact

### Continuous Deployment
- Practice of frequently delivering values through automated deployment process.
- Include: provisioning & creating infrastructure, smoke testing, promoting to production ,rollback, etc.

### The CI/CD Pipeline

![](https://video.udacity-data.com/topher/2020/July/5f0c9a06_screen-shot-2020-07-13-at-10.26.22-am/screen-shot-2020-07-13-at-10.26.22-am.png)

**Stages:** categories of jobs within the CI/CD pipelines:
- **Build**: Everything that has to do with making code executable in Production
- **Test**: Run alll automated tests that verify the code level
- **Analyze**: any sttic analysis on the code/checking dependencies
- **Deploy**: Anything to do with creating server instances or copying pre-built application files to an instance.
- **Verify**: any test that can be run against a running instance of the application, often against a pre-production instance.
- **Promote**: replace the current production environment with the new versions.
- **Revert**: Roll back/undo changes when the verification fails.

**Jobs:** sets of instructions to do the work of CI/CD + environments where the instructions are performed.
**Steps:** instructions within the jobs. Also have environments to run.

## <a id="benefits-of-ci/cd"></a>Benefits of CI/CD
It's crucial to be able to communicate with business and stakeholders. Use the `Values Framework` for the best translation.

**Values Framework** - includes one of these four terms when communicating with stakeholders: `reduce cost`,`avoid cost`,`increase revenue`, `protect revenue`

Examples:

![image](https://github.com/user-attachments/assets/d79fc0a6-bacd-4bc4-9622-c95417126398)

![image](https://github.com/user-attachments/assets/921158b1-a625-48f0-b0a7-e42810809816)

## <a id="best-practices"></a>Best Practices
- `Fail Fast`- set up CI/CD to find failures. The faster we find them, the quicker we fix them.
- `Measure quality`- Measure code quality so we evaluate if the codes are high quality
- `Only Road to Production`- if CI/CD is deploying to Production, it should be the only way -> easier to manage and improve and monitor.
- `Config in code` - configuration coddes must be in code and versioned alongside your production code. This includes CI/CD configuration files.


## <a id="deployment-strategies"></a>Deployment Strategies
- `Big Bang` - also known as no strategies at all, simply replacing old versions with new versions.
  - Pros: simplest to understand and perform
  - Cons:
      - Downtime when replacing old version with new version
      - Encrouages teams to batch up cahnges into a large deploy event -> require more testing -> slower to market
- `Blue Green` - Two Production versions: old version (Blue) and new version (Green). Traffics are routed to old version while the new version is being tested. Once the test is completed, all traffic are routed to the new version (Green).
  - Pros: fast rollback, no disturbance to the old version
  - Cons: high infrastructure cost
- `Canary` - Similar to `Blue Green` deployment. When the new version is deployed, traffics still route users to the versions. The router will slowly direct a small amount of traffic to the new version while the team monitors the new version. Slowly, the traffics are all routed to new versions.
  - Pros: easy to roll back and damage only affect a small portion of users
  - COns: High infrastructure cost and difficult to set up and maitain
- `A/B Testing` - Test the new version with a set of users. Once we get the users' feedbacks, we can decide to adapt the new version or roll back to the old version
  - Pros: Get direct feedbacks from users
  - Cons: difficult to set up & high cost method of User Acceptance Testing.

## <a id="blue-green"></a>Blue Green Deployment
### The router: 
- Key mechanism that directs traffics to new/old version depending on configurations.
    - Load Balancer: let us switch from front end to back end immediately
    - CDN: Offer a way to switch files immediately
    - DNS: common route but slow process due to DNS propagation and long TTL.
### Blue Green Deployment sequence:
1. `Compile`: Compile and create artifact
2. `Run Tests`: Run unit and/or integration tests
3. `Provision`: create Green infrastructure, cofiguring instances, migrating DB, etc.
4. `Deploy`: Copy artifact files to instance
5. `Smoke Test`: Run a few tests that don't impact the production servers
6. `Switch The Router`: Redirect traffic to new version
7. `Run Sanity Test`: Run a few tests that don't impact the productions servers
8. `Roll back` / `Destroy Old Realeas Environment`: if failed, switch the router back to the Blue version and clean up Green. Otherwise, clean up Blue environment and switch traffics to Green.
9. `Notify The Team`: Confirm that the deployment is successful.

## <a id="key-terms"></a>Key terms
- **Pipeline:** A series of automated steps that build, test, and deploy software changes from development to production
- **Continuous Integration:** The practice of merging all developers' working copies to a shared mainline several times a day.
- **Continuous Delivery:** An engineering practice in which teams produce and release value in short cycles.
- **Continuous Deployment:** A software engineering approach in which the value is delivered frequently through automated deployments.
- **Infrastructure as Code:** The management of infrastructure using code.
- **Provisioning:** The process of setting up IT infrastructure.
- **Artifact:** A product of some process applied to the code repository.
- **DevOps:** A set of practices that works to automate and integrate the processes between software development and IT teams.
- **Testing:** A practice that seeks to ensure the quality of the software.
