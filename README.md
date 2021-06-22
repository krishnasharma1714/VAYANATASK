# VAYANA-TASK
PROJECT
#######################  images ############

Dokcerfile_flask
Dockerfile_nginx

1) made EC2 insatnce 
2) installed docker  (https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9)
3) ran docker dameons 
4) make 2 images :myflask , myngnix  with above 2 docker files 

###########  Docker compose ######

files name : docker-compose.yml

1) install docker compose (https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9   OR  https://docs.docker.com/compose/install/)
2) make the 2 pods with this dokcer compose file using images which created privios task 
3) to check from local system :  curl -X GET 0.0.0.0:80   ( it will give output properly )

Output should be like :
[root@ip-172-31-58-62 ~]# curl -X GET 0.0.0.0:80
Hello VAYANA!


######### terraform work prerequisite ######

1) aws cli should be configured on your windows system and your aws account should be configured/attache  with it (https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html)
2) terraform exe should be conconfigured (https://www.terraform.io/downloads.html OR https://k21academy.com/terraform-iac/terraform-installation-overview/)



######## making ECR and ECS follow steps ########

we need to do below task with terraform
1) make repo
2) push iamges to repo ( it is manul not in terraform)
3) create cluster
4) create tasks
4) create service 
5) create networking 
6) create load balancer
7) create targate groups 


for every task in terraform ,there is a comment on above each task , please take referance through it 


make/copy/pull : main.tf and save it.

first run the below commands:
terraform init    : it will downoads aws packge/api 
terraform apply -target aws_ecr_repository.my_flask
---
do the below step : we need to copy our flask image into the repo--


2) push your repo into the repo you can use belwo steps 
 a) install aws cli on your ec2 and configure your account
 b) run below commands : you can find these commands in your repo section on aws because repo id will changes every time you create new repo
 
 change the repo id in all comands:
	
	aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 979577199360.dkr.ecr.eu-west-2.amazonaws.com
	docker tag myflask:latest 979577199360.dkr.ecr.eu-west-2.amazonaws.com/my-flask:latest     
	docker push 979577199360.dkr.ecr.eu-west-2.amazonaws.com/my-flask:latest


after above commands please check your flask image should be there in the aws ECR

3) then run full terraform apply
	terraform plan   --- for dry run  
	terraform apply  
	
	it will succ and give you LB DNS name , you can paste it in browser and hit it.

please let me know for any concern.
