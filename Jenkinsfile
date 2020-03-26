def pipelineContext = [:]
node {
    def registryProjet ='registry.gitlab.com/youssouy/docker-gitlab'
    def IMAGE= "${registryProjet}:version-${env.BUILD_ID}"
    
      stage ('Clone') {
          git 'https://github.com/OusmanaTraore/war-build-docker.git'
      }
      stage ('Maven package') {
          sh ' mvn package'
      }
      def img = stage ('Build') {
          docker.build("$IMAGE", '.')
         
      }
      stage ('Run'){
          img.withRun("--name run-$BUILD_ID -p 8082:8080") { c ->
          sh 'docker ps'
          sh 'netstat - ntaup'
          sh 'sleep 3s'
          sh 'curl 192.168.56.1:8082'
          sh 'docker ps'
          
      }
}
}
