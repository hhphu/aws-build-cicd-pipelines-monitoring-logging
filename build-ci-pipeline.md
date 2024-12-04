# Building a Continuous Integration Pipeline

1. Introduction
2. Building blocks of CI
3. Continuous Integration Tools

## Introduction
**Continuous Integration (CI)** is a software engineering practice in which chagnes to code are automatically integrated to shared repository on a regular basis.

Continuous Integation is important to:
- Improve the quality of software
- Catch errors early to fix them
- Make it easier to merge changes from multiple developers.

## Building blocks of CI
- **`Checkout`**: retrieve the most recent version of the code from a share repository.
- **`Build`**: compile codes, convert codes to binaries and executalbe files.
- **`Test`**: Automated test to make sure the codes functions as expected. Include unit, integration and end-to-end tests
- **`Lint`**: Analyze codes with potential errors, bugs and compliances
- **`Scan`**: scan for security issues: vulnerabilities, compliance, misconfiguration, vulnerable dependencies
- **`Notify`**: inform the team the outcome of the pipelines.

## Continuous Integration Tools
- Provide consistent + building environments for testing, building and deploying codes
- Being able to scale up/ scale down depending on projects
- Automation -> less human errors
- Some common CI tools: Jenkins, Travis CI, Github Actions, AWS Code Pipeline, Google Cloud Build, Azure Pipeline & Test plan
- To choose the right tool:
    - Compability and Integration: the tool places well with current softwares and tools -> seamless integration
    - Easy to use: The tools should be easy to use
    - Scalability & Performance: Allow you to scale up with big projects
    - Cost, Security and Compliance: These are also variables to consider when choosing CI tool for your team.
 
## Branching strategies
#### RELEASE-CENTRIC branching
- Organize codes around release cycles -> clear structure for managing releases.
    - Developers work on featured branches (branched from Development branch). Once they're done, the codes are merged back to the Development branch.
    - Release plan: A Release branch merges the code from the Development branch for final rounds of testing and bug fixes.
    - Post release: Merge the the release branch into the main branch on Production.
    - Hot fixes: provide bug fixes and merge directly into the main branch.
- Pros:
    - Provides clear structure for managing releases
    - Support parallel developemnt for features and bug fixes
    - Seperate releases and development prepartion
- Cons:
    - Complex for smaller projects/teams
    - Require strict workflow -> less flexibility
 
#### FEATURE-ORIENTED branching
- Emphasize developing individual features. separating them from the main branch.
- Enable parallel development and simplify code management and review.
- Workflow:
    - Create a new branch for each feature
    - Create a pull request to merge into the main branch once completed.
    - Ensure the main branch remains stable after merging.
- Pros:
    - Isolate works -> easier to manage and code review
    - Support parallel on multiple features development -> prevent blocking other features
    - Keeps the primary branch clean, ensuring integration of only vetted and tested code.
- Cons:
    - Require diligent branch management to avoid confusion and maintain the main branch clean
    - Can be challenging if the feature branch is not up to date compared to the main branch.
  
