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
	}
}
