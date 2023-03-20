@Library('cicd-task-lib@rohitkothapalli')_


            
pipeline {
            
    agent {
        node {
            label "agent1"
        }
    }
 tools {
        maven '3.9.1'
    }
     stages {
            stage('Packaging files to Executable Applications...........') {
            steps {
                mavenBuild('pom.xml', '-Xmx2g')
            }
        } 
       stage('Building Image and Pushing Into Artifactory.......') {
      steps {
        dockerBuild(
          dockerfilePath: '/home/jenkins/agent/workspace/cicdtask/Dockerfile',
          dockerImageName: 'my-docker-image',
          dockerImageTag: '1.0.1',
          dockerRegistryUrl: 'https://registry.hub.docker.com/',
          dockerRegistryUsername: 'krvnb',
          dockerRegistryPassword: 'RohiT.123'
        )
      }
    }
     stage('Deploying Application......') {
      steps {
        script {
          deploy(
              
            namespace: 'cicdtask',
            deploymentName: 'my-app',
            yamlFilePath: '/home/jenkins/agent/workspace/cicdtask/Deployments/values.yaml'
    
          )
        }
      }
    }
  }
}

