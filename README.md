# Docker Jenkins with nodejs :desktop_computer:

# :waving_black_flag:
### 1 STEP
```shell
dokcer build -t DOCKER_IMAGE_NAME .
```

### example command

```shell
docker build -t saurabharch/jenkins-blueocen_1.25.8:latest .
```

### 2. STEP
#### Create network

```shell
docker network create jenkins
```

### 3. STEP
#### Deployment

```shell
docker run --name jenkins --restart=on-failure --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/var/jenkins_home  --volume jenkins-docker-certs:/certs/client:ro --publish 8080:8080 --publish 50000:50000 saurabharch/jenkins-blueocen_1.25.8:latest
```

here jenkins-docker-certs stand as certifcate SSL certificate directory

#### Unlocking Jenkins
### 4.STEP

When you first access a new Jenkins instance, you are asked to unlock it using an automatically-generated password.

1. Browse to http://localhost:8080 (or whichever port you configured for Jenkins when installing it) and wait until the Unlock Jenkins page appears.

### 5. STEP

```shell
docker logs <docker-container-name>
```

### :man_in_lotus_position: Note:

    The command: sudo cat /var/lib/jenkins/secrets/initialAdminPassword will print the password at console.
    
    If you are running Jenkins in Docker using the official jenkins/jenkins image you can use sudo docker exec ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword to print the password in the console without having to exec into the container.

    On the Unlock Jenkins page, paste this password into the Administrator password field and click Continue.
    Notes:
    
    You can always access the Jenkins console log from the Docker logs (above).
    
    The Jenkins console log indicates the location (in the Jenkins home directory) where this password can also be obtained. This password must be entered in the setup wizard on new Jenkins installations before you can access Jenkins’s main UI. This password also serves as the default administrator account’s password (with username "admin") if you happen to skip the subsequent user-creation step in the setup wizard.

### :umbrella_on_ground: Customizing Jenkins with plugins
After unlocking Jenkins, the Customize Jenkins page appears. Here you can install any number of useful plugins as part of your initial setup.

Click one of the two options shown:

Install suggested plugins - to install the recommended set of plugins, which are based on most common use cases.

Select plugins to install - to choose which set of plugins to initially install. When you first access the plugin selection page, the suggested plugins are selected by default.

The setup wizard shows the progression of Jenkins being configured and your chosen set of Jenkins plugins being installed. This process may take a few minutes.

Creating the first administrator user
Finally, after customizing Jenkins with plugins, Jenkins asks you to create your first administrator user.

When the Create First Admin User page appears, specify the details for your administrator user in the respective fields and click Save and Finish.

When the Jenkins is ready page appears, click Start using Jenkins.
Notes:

This page may indicate Jenkins is almost ready! instead and if so, click Restart.

If the page does not automatically refresh after a minute, use your web browser to refresh the page manually.

If required, log in to Jenkins with the credentials of the user you just created and you are ready to start using Jenkins!

