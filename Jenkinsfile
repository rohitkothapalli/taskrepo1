@Library('cicd-task-lib@rohitkothapalli')_


            
pipeline {
            
    agent {
      kubernetes {
      label "agent1"
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock    
        '''
    }
//         node {
//             label "agent1"
//         }
    }
//     agent {
//     kubernetes {
//       yaml '''
//         apiVersion: v1
//         kind: Pod
//         spec:
//           containers:
//           - name: maven
//             image: maven:alpine
//             command:
//             - cat
//             tty: true
//           - name: docker
//             image: docker:latest
//             command:
//             - cat
//             tty: true
//             volumeMounts:
//              - mountPath: /var/run/docker.sock
//                name: docker-sock
//           volumes:
//           - name: docker-sock
//             hostPath:
//               path: /var/run/docker.sock    
//         '''
//     }
//   }
//  tools {
//         maven 'maven'
//         dockerTool 'docker'
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

