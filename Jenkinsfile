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
			kubecreds = 'kubecreds'
			dockerImage = ''
			backendReleaseName = "backend"
			frontendReleaseName= "frontend"
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
 		            script
 		            {
 		                sh ('git diff --name-only --diff-filter=ADMR @~..@ > output.txt')
                        def changedFiles = readFile 'output.txt'
                        echo "Changed files - ${changedFiles}"
 		            }

 		        }
 	        }
//  	        stage("helm upgrade")
//  	        {
//                 steps
//                 {
//                     script
//                     {
//                         withKubeConfig([credentialsId: kubecreds,
//                         serverUrl: "${serverUrl}"])
//                         {
//                             sh "kubectl cluster-info"
//                         }
//                     }
//                 }
//  	        }
 	        stage("install backend")
 	        {
 	            steps
 	            {
 	                script
 	                {
 	                    withKubeConfig([credentialsId: kubecreds,
                        serverUrl: "${serverUrl}"])
                        {
//                             installBackend(backendReleaseName)
                            if(changedFiles.contains("backend"))
                            {
                                echo "hello"
                            }
                            else
                            {
                                echo "not found"
                            }
                        }
 	                }
 	            }
 	        }
//  	        stage("install frontend")
//  	        {
//  	            steps
//  	            {
//  	                script
//  	                {
//  	                    withKubeConfig([credentialsId: kubecreds,
//                         serverUrl: "${serverUrl}"])
//                         {
//                             installfrontend(frontendReleaseName)
//
//                         }
//  	                }
//  	            }
//  	        }

      }

}
def installBackend(backendReleaseName){
    script
    {
        sh ("helm upgrade --install ${backendReleaseName} ./backend --set imageCredentials.username=${docker_username} --set imageCredentials.password=${docker_password} --set bucketname=${s3_bucket} --set awsAccessKey=${access_key} --set awsSecretKey=${secret_key} --set redis.password=${redis_password} --set dbsecret.rdsurl=${rds_url} --set replicaCount=2")
    }
}

def installfrontend(frontendReleaseName){
    script
    {
        backendSvcName = sh (returnStdout: true, script: "kubectl get service -n api| grep api-backend | awk '{print \$1}'| tr -d '\n'")
        sh ("helm upgrade --install ${frontendReleaseName} ./frontend/ --set backendServiceName=${backendSvcName} --set imageCredentials.username=${docker_username} --set imageCredentials.password=${docker_password}")
    }
}
