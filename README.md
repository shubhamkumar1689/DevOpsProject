# DevOpsProject

1. Create a container image that has Linux and other basic configuration required to run Slave for Jenkins. ( example here we require kubectl to be configured ) . For that, you will use this Dockerfile I have created.



2. When we launch the job it should automatically start the job on slave based on the label provided for a dynamic approach. For that, you need to install Docker plugin inside Jenkins. And do the following configuration : -


Now you need to specify the container image with label so we can identify similar jobs to be run on that container. And remember we want an image which has kubectl configured which we have already created in the first step.

3. Creating a job chain Pipeline of Job1 and Job2


4.Job1 : Pull the Github repo automatically when some developers push repo to Github and perform the following operations as:
4.1 Create the new image dynamically for the application and copy the application code into that corresponding docker image
4.2 Push that image to the docker hub (Public repository)
( Github code contain the application code and Dockerfile to create a new image )




Jenkins is using the GIT POLL SCM method where I have exposed my IP address by creating a tunnel for port 8080 of Jenkins using ngrok . So as soon as Developer pushes the code, GitHub notifies Jenkins through ngrok tunnel, in response Jenkins runs this job (Job1) which is to download the code, publish the image having an application code already copied in it.



5. Job2 ( Should be run on the dynamic slave of Jenkins configured with Kubernetes kubectl command): Launch the application on the top of Kubernetes cluster performing following operations:
5.1 If launching the first time then creates a deployment of the pod using the image created in the previous job. Else if deployment already exists then do a rollout of the existing pod making zero downtime for the user.
5.2 If Application created the first time, then Expose the application. Else don’t expose it.
