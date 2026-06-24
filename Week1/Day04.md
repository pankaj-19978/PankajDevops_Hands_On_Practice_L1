# Day 04 - more packages, Key pair , Service

## 🔹 Ansible - Install Multiple Package

---
 - name: Install packages for pathnex
   hosts: all
   becomes: yes

   tasks:
      - name: install tools
        yum:
         name:
           - git
           - wget
         state: present


## 🔹 Terraform - EC2 With Key Pair  (c6i.8xlarge)

        provider "aws" {
           region = "us-east-1"
        }

        resource "aws_key_pair" "pathnexkey" {
           key_name  = "pathnexkey"
            public_key = "ssh-rsa AAAA...."
         }

         resource "aws_key_instance" "pathnexEC2" {
           ami  = "ami-0abcd1234abcd1234"
           instance_type = "c6i.8xlarge"
           key_name = aws_key_pair.pathnexkey.key_name

           tags =  {
             name = "pathnex-EC2"
           }
        }


##  🔹 Kubernetes - Create ClusterIP Service

     apiversion: v1
     kind: service
     metadata:
         name: pankaj-service
     spec:
      selector:
        app: pankaj-app
      ports:
        - ports: 80
          targetport: 80


# Parallel Builds
##  🔹 Jenkins pipeline - parallel Build & Test
you Will learn how to ** run build and test in parallel**.

   pipeline {
       agent any
       stages {
          stage('parallel Tasks') {
             parallel {
                 stage('Build')   {
                    steps {
                       sh 'mvn clean compile'
                    }
                  }
                  stage('Test') {
                     steps {
                         sh 'mvn test'
                     }
                  }
               }
            }
         }
     }

##  🔹 Gitlab CI- Parallel JObs
you will learn how to **run parallel jobs in Gitlab CI**.
  stages:
    - build-test


  maven-build:
    stage: build-test
    image: maven:3.8.1-jdk-17
    script:
       - cd sample-java-app
       - mvn test
     parallel: 1

                    
