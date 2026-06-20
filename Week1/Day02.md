# Day 02 - Services & Tags

## 🔹Ansible - Install & Enable Nginx

---
 - name: Install and start Nginx on Local machine
   hosts: all
   become: yes

   task:
    - name: install nginx
      yum:
        name: nginx
        state: present

    - name: enable nginx
      service:
         name: started
         enabled: yes



## 🔹Terraform - EC2 with tags (r5.2xlarge)

     provider "aws" {
        region = "us-east-1"
     }

     resource "aws_instance" "pankajec2" {
       ami           = "ami-0abcd1234abcd1234"
       instance_type = "r5.2xlarge"

       tags = {
         Name        = "pankaj-server"
         Environment = "Training"
         Owner       = "pankajstudent"
       }
     }


## 🔹Kubernetes - Deployment with 2 Replicas

     apiversion: apps/v1
     kind: Deployment
     metadata:
       name: pankaj-deployment
     spec:
       replicas: 2
       selector:
         matchlabels:
           app: pankaj-app
       template:
         metadata:
           labels:
             app: pankaj-app
       spec:
         containers:
           - name: app
             image: nginx
             ports:
               - containerport: 80



## 🔹shell script - disk usage
#!/bin/bash
df -h


#Maven Build
## 🔹jenkins pipeline - maven Build
you will learn how to **compile, test,and package a java project**

   pipeline {
       agent any
       tools {
           maven 'maven-3.8.1'
           jdk 'jdk-17'
       }
       stages {
           stage('checkout') {
               steps {
                   git url: 'https://github.com/Pathnex/sample-java-app.git'
               }
       }
       stage('compile') {
           steps {
               sh 'mvn clean compile'
           }
       }
       stage('Test') {
           steps {
               sh 'mvn test'
            }

       }
       stage('package') {
           steps {
               sh 'mvn test'
            }
       }
       stage('package') {
           steps {
               sh 'mvn package'
            }
       }
    }
 }



## 🔹Gitlab CI - Maven Build

       stages:
         - build
         - test
         - package


       maven-build:
         stage: build
         image: maven:3.8.1-jdk-17
         script:
           - git clone  https://github.com/Pathnex/sample-java-app.git
           - cd sample-java-app
           - mvn clean compile
        maven-test:
          stage: test
          image: maven:3.8.1-jdk-17
          script:
             - cd sample-java-app
             - mvn test
        maven-package:
          stage: package
          image: maven:3.8.1-jdk-17
          script:
             - cd sample-java-app
             - mvn package
   
      

