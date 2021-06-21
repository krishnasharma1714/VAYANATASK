# VAYANATASK
PROJECT
#######################  images ############

Dokcerfile_flask
Dockerfile_nginx

1) made EC2 insatnce 
2) installed docker  (https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9)
3) ran docker dameons 
4) made 2 images with above 2 files : iamges name :  myflask , my ngnix 

###########  Docker compose ######

files name : docker-compose.yml

1) install docker compose (https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9   OR  https://docs.docker.com/compose/install/)
2) make the 2 pods with this dokcer file 
3) to check from local system :  curl -X GET 0.0.0.0:80   ( it will give output properly )



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
6) creat load balancer


for every task in terraform ,there is a comment on above each task , please take referance through it 

1) first run only 2 comments code :
####### provider ####
######  creation of 2 ECR repo  #######

2) push your repo into the repo you can use belwo steps 
 a) install aws cli on your ec2 and configure your account
 b) run below commands 
	aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 979577199360.dkr.ecr.eu-west-2.amazonaws.com
	docker tag myflask:latest 979577199360.dkr.ecr.eu-west-2.amazonaws.com/my-flask:latest   
	docker push 979577199360.dkr.ecr.eu-west-2.amazonaws.com/my-flask:latest
	docker tag nginx:latest 979577199360.dkr.ecr.eu-west-2.amazonaws.com/nginx:latest
	docker push 979577199360.dkr.ecr.eu-west-2.amazonaws.com/nginx:latest

3) after running these 2 steps run below comments code:
###### make cluster #####
######## role for ECS ###########
####### policy for role ######
###### attached the role ########
######### make our flask task defination #########
######### make our nginx task defination #########
#############  flask service #####
#############  nginx service #####
#### using  defult VPC/subnets companant  #########
##########   referncing flask service  to the subnets ####
##########   referncing nginx service  to the subnets ####
##### making load balncer #######
#### Creating a security group for the load balancer ########
####### directing  traffic, making  target group and listener ####
#####  creating security group ##



you can run it as dry run first the apply 
