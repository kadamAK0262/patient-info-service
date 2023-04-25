pipeline{

	agent any

		stages{

			stage('Checkout'){

					steps{

						git branch: "main", url: 'https://github.com/kadamAK0262/patient-info-service.git'

						}

					}

			stage('Build'){

					steps{

						sh 'chmod a+x mvnw'

						sh './mvnw clean package -DskipTests=true'

						}

					post{

						always{

							archiveArtifacts 'target/*.jar'

							}

						}

				}

			stage(DockerBuild) {

						steps {

							sh 'docker build -t -f akshayak0262/patient-basicinfo-service:latest .'

							}

						}

			stage('Login') {

					steps {

						sh 'echo Akshay@0262 | docker login -u akshayak0262 --password-stdin'

						}

					}

			stage('Push') {

					steps {

						sh 'docker push akshayak0262/patient-basicinfo-service'

						}
	
					}

				}

		post {

			always {

				sh 'docker logout'

				}

			}

}
