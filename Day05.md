# Day 05 - Handler, User-Data, Resource Limits

## 🔹 Ansible - Handler to Restart Nginx

---
 - name: manage nginx
   hosts: all
   become: yes

   tasks:
     - name: update config file
       copy:
         src: index.html
         dest: /usr/share/nginx/html/index.html
        notify: Restart nginx

    handlers:
      - name: Restart nginx
        service:
           name: nginx
           state: restarted


## 🔹 Terraform - EC2 with user data (c6a.12xlarge)

    resource "aws_ instance" "PankajEC2" {
      ami         = "ami-0abcd1234abcd1234"
      instance_type = "c6a.12xlarge"

      user_data = <<EOF
     #!/bin/bash
     yum install -y httpd
     systemctl start httpd
    

     EOF

       tags = {
         Name = "pankaj-EC2"
       }
     }


## 🔹 kubernetes - Resource Limits

      apiversion: v1
      kind: pod
      metadata:
          name: pankaj-limited-pd
      spec:
        container:
          - name: app
            image: nginx
            resources:
               limits:
                 memory: "256mi"
                 cpu: "500m"

# Day 05 - Environment variables

##  🔹 jenkins pipeline - use Environment variables
you will learn how to **use environment variables in jenkins pipelines**

    pipeline {
        agent any
        environment {
            INSTITUTE_NAME = "pathnex"
        }
        stages {
            stage('Print) {
                steps {
                    sh 'echo "WELCOME to $institute_name Devops Training"'
                }
            }
            stage('BUild') {
                steps {
                    sh 'mvn clean package -Dinstitute.name=$Institute_name'
                }
            }
         }
      }


##  🔹 Gitlab CI - Use Environment Variables
you will learn How to ** Use CI Variables IN Gitlab Pipelans**.


     stages:
        - build
     variables:
       institute_Name: "pathnex"
     build:
       stage: build
       image: maven:3.8.1-jdk-17
       script:
         -  git clone https://github.com/Pathnex/sample-java-app.git
         -  cd sample-java-app
         -  echo "welcome to $institute_Name Devops Training"
         -  mvn clean package -Dinstitute.name=$Institute_name

            

