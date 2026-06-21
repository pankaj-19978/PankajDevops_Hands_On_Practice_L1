# Day 03 -Users, SGs, ENV Vars

## 🔹 Ansible - Create User

---
 - name: Create pankaj user
   hosts: all
   become: yes

   tasks:
     - name: create user pankaj-admin
       user:
         name: pankaj-admin
         shell: /bin/bash


## 🔹 Terraform - Security Group  (r6i.4xlarge EC2)

   provide "aws" {
     region = "us-east-1"
   }

   resource "aws_security_group" "PankajSG" {
      name       = "PankajSG"
      description = "pankaj SG for SSH"

      ingress {
         from_port  = 22
         to_port    = 22
         protocol   = "tcp"
         Cidr_blocks = ["0.0.0.0/0"]
      }
   }

   resource "aws_instance" "pankajEC2" {
     ami                    = "ami-0abcd1234abcd1234"
     instance_type          = "r6i.4xlarge"
     vpc_security_group_ids = [aws_security_group.pankajsg.id]

     tags = {
       Name = "pankaj-EC2"
       }
     }


## 🔹 kubernetes - Add Environment Variables

      apiversion: v1
      kind: pod
      metadat:
        name: pankaj-env-pod
      spec:
        containers:
          - name: app
            image: nginx
            env:
              - name: APP_ENV
                value: "production"


## 🔹 Shell script - Check file exists
   #!/bin/bash
   File="/tmp/pankaj.txt"


   if [ -f "$File" ]; then
      echo "file exists"
   else
      echo "File Does not exist"
   fi


# Nodejs Build
## 🔹 Jenkins Pipeline - Nodejs Build
you will learn how to **install dependencies, run tests, and build a nodejs project**.
   pipeline  {
       agent any
       tools {
           nodejs 'Nodejs-16'
       }
       stages {
          stage('Checkout') {
             steps {
                git url: 'https://github.com/Pathnex/sample-node-app.git'
             }
          }
          stage('install Dependencies') {
             steps {
                 sh 'npm install'
             }
          }
          stage('run Tests') {
             steps {
                sh 'npm test'
             }
          }
          stage('Build') {
              steps {
                  sh 'npm run build'
             }
          }
     }
 }


## 🔹 Gitlab CI - Nodejs Build

      stages:
         - install
         - test
         - build

       node-install:
         stage: install
         image: node:16
         script:
            - git clone https://github.com/Pathnex/sample-node-app.git
            - cd sample-node-app
            - npm install

        node-test:
          stage: test
          image: node:16
          script:
             - cd sample-node-app
             - npm test

         node-build:
            stage: build 
            image: node:16
            script:
               - cd sample-node-ap       
               - npm run build
