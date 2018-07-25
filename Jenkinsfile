stage('Containers em Execução') {
  steps {
    node('master') {
      sh "for i in \$( docker ps -q ); do docker inspect \$i | grep -w Hostname | awk -F \\\" '{print \$4}' ;done > /tmp/Containers"
      sh "cat /tmp/Containers"    
    }
  }
}

stage('Teste Slave') {
  steps {
    node('slave') {
      sh "for i in \$( ls /srv/compose );do docker-compose -f \$i ps | awk '{if (NR!=1) {print \$1}}' | awk -F '---' '{print \$1}' | tr '\n' ' '; done"
    }
  }
}
