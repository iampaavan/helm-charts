pipeline
	{
	  environment
	  {
			registry = credentials("docker_registery")
			docker_username = credentials("user_name")
		    docker_password = credentials("password")
		    s3_bucket = credentials("bucketname")
		    access_key = credentials("aws_access_key")
		    secret_key = credentials("aws_secret_key")
		    rds_url = credentials("rds_url")
		    redis_password = credentials("redis_password")
		    serverUrl = credentials("serverUrl")
			registryCredential = 'dockerhub'
			githubCredential = 'github'
			kubeconfig = 'kubernetes_config'
			dockerImage = ''
			GIT_COMMIT = """${sh(
                returnStdout: true,
                script: 'git rev-parse HEAD'
            ).trim()}"""
	  }
	  agent any
	  stages
	  {
 			stage('Git Checkout')
 			{
 			    steps
 		        {
 		            checkout scm
 		        }
 	        }
 	        stage("helm upgrade")
 	        {
                steps
                {
                    script
                    {
                        sh ("pwd")
                        sh ("ls")
                        withKubeConfig([credentialsId: kubeconfig,
                        serverUrl: "${serverUrl}"])
                        {
                            sh "kubectl cluster-info"
                        }
                    }
                }
 	        }
      }

}
