# SSIS Configuration Override Causing Connection Failure

## Context

An ETL workflow failed during execution due to a database connectivity issue.
The SSIS Project was deployed using the Project Deployment Model with environment based parameter configuration.

## Observed Symptoms

-Execution Failed during connection validation.

-database connection could not be established.

-Workflow terminated before the data extraction phase.

## Investigation

1.Reviewed SSIS catalog execution reports to confirm the connection failure.

2.Verified that the originally referenced server endpoint was no longer accessbile.

3.Updated the connection manager value within the SSIS package and redeployed the project.

4.Re-executed the workflow - failure persisted.

5.Analyzed project-level parameters in SSISDB.

6. Identified that a project parameter was mapped to an environment variable.

7. Confirmed that the runtime environment variable was overriding the package-level configuration.

## Root Cause

Although the connection manager was updated in the package,the deployed project was configured to use environment-level parameter mapping.
The environment variable still referenced an outdated server endpoint,causing the connection failure at runtime.

## Resolution

-Updated the environment variable in SSIS catalog to reference the correct server.

-Validated parameter-to-environment bindings.

-Re-executed successfully.

-Monitored subsequent executions to confirm stability.

## Engineering Insight

In the SSIS Project Deployment Model,environment variables can override package-level configuration at runtime.
Effective troubleshooting requires validating the complete configuration hierarchy,including project parameters and environment references.
