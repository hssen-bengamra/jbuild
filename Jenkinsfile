def pipelineContext = [:]
node {

   def registryProjet='registry.gitlab.com/ws5802227/test'
	 def IMAGE="${registryProjet}:version-${env.BUILD_ID}"

	 echo "IMAGE = $IMAGE"

    stage('Clone') {
    			checkout scm
		}

		def img = stage('Build') {
					docker.build("$IMAGE",  '.')
		}
	
		stage('Run') {
					img.withRun("--name run-$BUILD_ID -p 8086:80") { c ->
					sh 'curl 172.18.0.1:8086'
          }					
		}

		stage('Push') {
					docker.withRegistry('https://registry.gitlab.com', 'reg1') {
							img.push 'latest'
              img.push()
					}
		}
 
}

