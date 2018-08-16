node {
    try {
        stage 'Checkout'
        checkout scm
        echo "Branch: ${env.BRANCH_NAME}"

        stage "Rebuild packages"
        sh "ls -c1 -d */ | xargs -n1 helm package"

        stage "Update index"
        sh "helm repo index ."

        stage "Push packages"
        sh "git config --global user.email 'you@example.com'"
        sh "git config --global user.name 'Your Name'"
        sh "git add ."
        def message = "New chart version : ${env.BUILD_NUMBER} - ${env.BRANCH_NAME}"
        sh "git commit -m '${message}'"
        sh "git push"

    } catch (err) {
        currentBuild.result = 'FAILURE'
        
    }
}


