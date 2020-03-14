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
			registryCredential = 'dockerhub'
			githubCredential = 'github'
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
//                         sh ("kubectl get nodes")
                        sh ('helm install release ./backend --set imageCredentials.username=hemalgadhiya --set imageCredentials.password=Hh07101996 --set bucketname=dev-hgadhiya-csye7374-image-upload --set awsAccessKey=AKIAUJWRCG77QYGIF35U --set awsSecretKey=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 --set redis.password=Admin@123 --set dbsecret.rdsurl=postgres-rds-instance.crhih3bwnzav.us-east-1.rds.amazonaws.com --set replicaCount=2')
                    }
                }
 	        }
      }

}
