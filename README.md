# Readme

We'll set up a single Jenkins master and agent with the following steps.

## Master

Run `docker-compose up -d` in the project directory, which will run the Jenkins master on `localhost:8080`.
Follow the given installation steps as usual; the administrator password may be seen in the Docker logs for the master container.

## Agent

#### Creating an agent

From the Jenkins home page, go to 'Manage Jenkins' >> 'Manage Nodes and Clouds'.
There, go to 'New Node' and create a new permanent agent called `agent`.
Set its remote root directory to `/home/jenkins`, and ensure that the launch method is set to 'Launch agent by connecting it to the master'.
The remaining configurations may be left as its defaults, or customised accordingly. Save the configuration.

#### Setup the agent

Go to the agent's status page, and copy the secret key to a new `.env` file in the local project directory.

```
AGENT_SECRET=<secret-key>
```

Re-run `docker-compose up -d`, which should boot up containers for and connect both the Jenkins master and agent.
Now jobs and pipelines may be run using the Jenkins agent node.

## Testing a Jenkins pipeline

The Jenkins pipeline may be tested using the provided `jenkins-test` repository (https://github.com/halfwhole/jenkins-test.git),
or through any custom Git repository of your own with a `Jenkinsfile` defined.

Create a new Pipeline or Multibranch Pipeline job. 
- For a Pipeline job, set the pipeline's definition to be 'Pipeline script from SCM', linking to the Git repo.
- For a Multibranch Pipeline job, set the Git repo under 'Branch Sources', and ensure that 'Build Configuration' is set 'by Jenkinsfile'.

The pipeline should work.
