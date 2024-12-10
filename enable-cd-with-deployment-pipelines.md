# Enabling Continuous Deliver with Deployment Pipelines

1. **[Delivery vs Deployment](#delivery-deployment)**
2. **[Building blocks in Continuous Delivery & Deployment](#building-blocks-cd)**
3. **[Github Environments](#github-environments)**
4. **[Deployment Strategies](#deployment-strategies)**
5. **[Blue Green Deployment](#blue-green)**
6. **[Key Terms](#key-terms)**

## <a id="delivery-deployment"></a>Delivery vs Deployment
Two practices that help teams deliver high quality softwares to their users.

**Continuous Delivery**
Ensure software is always is in releasable state by frequenlty building, testing and validating changes.
Great fit for teams that want to release software frequently with high quality

Pros:
- Companies with strict compliance,requirements and regulations.
- Releases and updates that are tied to business events
  
Cons:
- Manual approval required -> slow down the process -> less releases -> slow down innovations.

**Continuous Deployment**
An automated processes where every change in the software, after being automatically tested and validated, will automatically deploys to production.

Pros:
- Best fit for rapid integration as approved codes are automatically deployed to Production
- Users feedback is quickly needed for response and implementation.
- For complex/distributed system where manual management is difficult.
  
Cons:
- More complex, automation and more robust testing
- Strong QA and monitoring to quickly detect errors
- Costly resources and infrastructures.

## <a id="building-blocks-cd"></a>Building blocks in Continuous Delivery & Deployment
**Version Control:** Maitain storage for artefact that are deployable 

**Environment Configuration:** Manage environemnt-specific configuration for testing and validations -> ensure successful deployment across environments.

**Deployment Strategies:** various technique implemented to minimize risks and downtime

**Monitoring & Observability:** log and monitor performance of the applications -> allows to detect error quickly to fix

**Fix Forward or Rollback:** When there's an issue, either push forward for fixes or roll back the deployment.

**Security & Compliance:** ensure compliance and security best practice are met, vulnerability scanning and access control.

## <a id="deployment-strategies"></a>Deployment Strategies

**All-at-once**- Deploy the updated application to all instances at once. It's quick and easy but comes with a high risk of downtime if deployment issues occur. Rolling back can also be a challenge.

**Rolling** - Deploy the new version incrementally, replacing one instance at a time. This minimizes downtime risk and simplifies rollback. However, it may prolong deployment times and cause potential version incompatibility.

**Blue-Green** - Maintain two identical production environments and switch traffic after deploying the new version to one. This strategy effectively mitigates downtime and facilitates rollback, albeit at the cost of higher resource usage and management complexity.

**Canary** - Release the new version to a small set of instances first, gradually directing traffic to it based on performance. This strategy gives controlled exposure to the new version and helpful feedback. It can be complex to execute and may lengthen the deployment process.

### Things to consider:
- **Projects requirements:** what's the project downtime tolerance, application complexity, etc.
- **Infrastructure & Resources:** what resources and tools are available, what would be the cost.
- **Risk Management:** What are the risks associated with the deployemnt strategies we consider.

  
