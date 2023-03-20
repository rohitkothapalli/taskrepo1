@Library('cicd-task-lib@rohitkothapalli')_


            
pipeline {
            agent any
//     agent {
//         node {
//             label "agent1"
//         }
//     }
     stages {
            stage('Packaging files to Executable Applications...........') {
            steps {
                mavenBuild('pom.xml', '-Xmx2g')
            }
        } 
       stage('Building Image and Pushing Into Artifactory.......') {
      steps {
        dockerBuild(
          dockerfilePath: '/Users/krvnbangarraju/.jenkins/workspace/cicd-task/Dockerfile',
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
            yamlFilePath: '/Users/krvnbangarraju/.jenkins/workspace/cicd-task/Deployments'
    
          )
        }
      }
    }
  }
}

