node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email devopssameera@gmail.com"
                    sh "git config user.name Sameera Dissanayaka"
                    sh "cat deployment.yml"
                    sh "sed -i 's+devopswithsam/jenkins-flask.*+devopswithsam/jenkins-flask:${DOCKERTAG}+g' deployment.yml"
                    sh "cat deployment.yml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push @github.com/${GIT_USERNAME}/avatar-k8s.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/avatar-k8s.git HEAD:main"
                }
            }
        }
    }
}