pipeline {
    agent any

    stages {
        stage('Get Repo') {
            steps {
                git credentialsId: '1042e461-8624-4992-b374-6b79b590a69d', url: 'https://github.com/Probablyall/example-playbook.git'
                ansibleVault(action:'decrypt', input:'secret', vaultCredentialsId: 'c5187f74-53a7-441f-b980-49384e6e045e')
                sh 'mv ./secret ~/.ssh/id_rsa'
                sh "chmod 400 ~/.ssh/id_rsa"
                sh "ansible-galaxy install -r requirments.yml -p roles"
                
            }
    
            }
        stage('Run Playbook'){
            steps {
                ansiColor('xterm'){
                    ansiblePlaybook(
                        playbook: "site.yml",
                        inventory: "inventory/prod.yml",
                        colorized: true)
                }
            }
        }
    }
}
