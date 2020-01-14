# airgapped-operator
POC for an ansible-based operator using env vars for images to be used in an airgapped environment

This is an example of a mongoDB k8s operator that
 1) uses Ansible
 2) passes an environment variable as the image used by the deployment
 
# What to look for

In the tasks/main.yaml, all images use

            containers:
            - name: mongodb
              image: "{{ lookup('env','RELATED_IMAGE_DB') | quote }}"
          
to reference images.

These environment variables are then defined and set to a default value in the operator.yaml:

          env:
            - name: RELATED_IMAGE_DB
              value: "registry.access.redhat.com/rhscl/mongodb-36-rhel7:latest"
