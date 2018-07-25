node('master') {
    checkout scm
    sh "for i in \$( docker ps -q ); do docker inspect \$i | grep -w Hostname | awk -F \\\" '{print \$4}' ;done > /tmp/Containers"
    sh "cat /tmp/Containers" 
}

node('slave') {
    try {
        sh "for i in \$( ls /srv/compose );do docker-compose -f \$i ps | awk '{if (NR!=1) {print \$1}}' | awk -F '---' '{print \$1}' | tr '\n' ' '; done"
    } catch (e) {
        currentBuild.result = 'ERRO AO EXECUTAR O COMANDO ACIMA'
        throw e
    } 
}
