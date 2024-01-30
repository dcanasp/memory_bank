Elastic container registry

where you store your docker containers, it's used for every place where you need a container like [[Lambda]]

Conecting:

the page gives you the instructions. but the first part is doing the configuration,

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 324433828909.dkr.ecr.us-east-1.amazonaws.com