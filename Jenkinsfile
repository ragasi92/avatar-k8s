node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github_credentials', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email ragasi1992@gmail.com"
                    sh "git config user.name Raul Garay"
                    sh "cat avatar.yaml"
                    sh "sed -i 's+ragasi1992/avatar-frontend-devops.*+ragasi1992/avatar-frontend-devops:${DOCKERTAG}+g' avatar.yaml"
                    sh "sed -i 's+ragasi1992/avatar-backend-devops.*+ragasi1992/avatar-backend-devops:${DOCKERTAG}+g' avatar.yaml"
                    sh "cat avatar.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                   // sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/avatar-k8s.git HEAD:main"
            }
        }
    }
}
}