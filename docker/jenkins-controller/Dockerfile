FROM --platform=linux/amd64 jenkins/jenkins:2.430-jdk21

USER root

RUN apt-get update -y && apt-get install -y \
    unzip \
    git \
    && rm -rf /var/lib/apt/lists/*

# copy the list of plugins to install
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt

# disable the setup wizard
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# copy the config-as-code yaml file into the image
COPY jenkins.yaml /usr/share/jenkins/ref/jenkins.yaml

# tell the jenkins config-as-code plugin where to find the yaml file
ENV CASC_JENKINS_CONFIG /usr/share/jenkins/ref/jenkins.yaml

COPY initialConfig.groovy /usr/share/jenkins/ref/init.groovy.d/initialConfigs.groovy

# create a sample job via XML
COPY job.xml /usr/share/jenkins/ref/jobs/serverless-jenkins-on-ecs/config.xml

USER jenkins