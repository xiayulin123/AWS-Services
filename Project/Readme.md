Using Jenkins maven ansible and kuburnetes

CI:
changes in github repo -> initiate the job trigger -> Jenkins pull the code from repo ->
build the artifact using maven -> push the artifact to ansible server -> create docker image using artifact -> copy the docker image to docker hub

-> trigger the CD job

CD:
boost server pull docker image from dockerhub -> build container for kubernetes -> finished