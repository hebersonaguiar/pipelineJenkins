node {
  checkout scm

  stage ('Containers em Execução') {
      sh "for i in \$( docker ps -q ); do docker inspect \$i | grep -w Hostname | awk -F \\\" '{print \$4}' ;done"    
  }
}
