node {
  checkout scm

  stage ('Containers em Execução') {
      sh script: "for i in $( ls /srv/compose );do docker-compose -f $i ps | awk '{if (NR!=1) {print $1}}' | awk -F --- '{print $1}' | tr '\n' ' '; done"    
  }
}
