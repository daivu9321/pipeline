pipeline {
    agent any 
    environment {
		DOCKERHUB_CREDENTIALS=credentials('Dockerhub')
        ANSIBLE_PRIVATE_KEY=credentials('Ansible_key')
	}
 
    stages {
		
        stage('Build') {

			steps {
				sh 'docker build -t daivudevops9321/pipeline:latest .'
			}
		}

		stage('Login') {

			steps {
				// sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                 sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push daivudevops9321/pipeline:latest'
			}
		}

        // stage('Deploy') { 
        //         steps {
        //         ansiblePlaybook become: true, credentialsId: 'EC2-privatekey', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory.ini', playbook: 'playbook.yaml'
        //          //sh 'ansible-playbook -i ./ansible/inventory.ini --private-key=$ANSIBLE_PRIVATE_KEY ./ansible/playbook.yaml'
      
        //     }
        // }
    *+++}
    post {
		always {
			sh 'docker logout'
		}
	}
}
