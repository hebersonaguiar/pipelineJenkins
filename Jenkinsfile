node('master') {
    stage('Containers em Execução') {
        checkout scm
        sh "for i in \$( docker ps -q ); do docker inspect \$i | grep -w Hostname | awk -F \\\" '{print \$4}' ;done > /tmp/Containers"
        sh "cat /tmp/Containers " 
        sh "rm -rf /tmp/Containers"
    }
}

node('slave') {
    stage('Docker Compose Containers') {
        try {
            sh "for i in \$( ls /srv/compose );do docker-compose -f /srv/compose/\$i ps | awk '{if (NR!=1) {print \$1}}' | awk -F '---' '{print \$1}' | tr '\n' ' '; done > /tmp/ContainersExec"
            sh "cat /tmp/ContainersExec"
            sh "rm -rf /tmp/ContainersExec"
        } catch (e) {
            currentBuild.result = 'ERRO AO EXECUTAR O COMANDO ACIMA'
            throw e
        } 
    }
}

node('master') {
    stage('Containers em Execução') {

        input 'Deseja continuar com a ação?'

        parameters {
            choice(
                choices: 'Continue\nAbortar',
                description: 'Deseja continuar com o upgrade?',
                name: 'REQUESTED_ACTION')
        }

        when {
            expression { params.REQUESTED_ACTION == 'Continue' }
        }

        steps {
            print "DEBUG: TESTE PARAMETRO TAG = ${params.Tag}"
        }
    }
}
