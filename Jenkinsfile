pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [[$class: 'CleanCheckout']], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[credentialsId: 'github-pass', url: 'https://github.com/domingo-ultratendency/kafka-cluster-ansible.git']]
                ])
            }
        }
        stage('Download Kafka source code') {
            steps {
                sh "wget https://dlcdn.apache.org/kafka/3.1.0/kafka_2.13-3.1.0.tgz"
            }
        }
        stage('Cluster Setup') {
            steps {
                sh "ansible-playbook -i inventory/development/cluster.ini clusterSetup.yml"
            }
        }
    }
}