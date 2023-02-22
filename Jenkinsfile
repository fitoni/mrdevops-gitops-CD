pipeline {
    agent any
    parameters {
        string(defaultValue: "", description: '', name: 'BUILDNUMBER')
    }
    environment{
        VERSION = "${BUILDNUMBER}"
    }
   
    stages{
        stage('Update latest tag in kubernetes deployment file in jenkins local worskpace'){
            steps{
                script{
                    //echo "=== ${VERSION} ==="
                    sh """
                        cat deploymentservice.yaml
                        sed -i 's+fitoni/mrdevops-gitops.*+fitoni/mrdevops-gitops:${VERSION}+g' deploymentservice.yaml
                        cat deploymentservice.yaml
                    """                       
                }
            }
        }

       /*  stage('Push updated kubernetes deployment file onto GitHub'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'github-account', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh """
                        git config user.email fitoni77@gmail.com
                        git config user.name fitoni
                        git add deploymentservice.yaml
                        git commit -m "Done by Jenkins Job changemanifest: ${VERSION}"
                        git push https://fitoni:${GIT_PASSWORD}@github.com/fitoni/mrdevops-gitops-CD.git HEAD:main
                    """     
                    }                    
                }
            }
        } */
    }
}
