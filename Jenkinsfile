pipeline {

	agent any

	/*
	environment {
	// define environmental variables
	// to be used in the next lines

		//Bind credentials into an environmental variable
		//SERVER_CREDENTIALS = credentials('<credentials>')

	}
	*/

	parameters {
	// define parameters

		// Types of parameters:
		// - string(name, defaultValue, description)
		// string(name: 'VERSION', defaultValue: '', description: 'Version to deploy')
		//
		// - choice(name, choices, description)
		choice(name: 'VERSION', choices: ['1.0.0', '1.0.1', '1.0.1a'], description: 'choice: version to deploy')
		//
		// - booleanParam(name, defaultValue, description)
		booleanParam(name: 'executeTests', defaultValue: true, description: 'boolean used to define if to execute tests')

	}
	
	stages {
	// The list of all stages
	
		stage('1 - git clone') {

			steps {
				script {
					echo '1: git clone'

					// Use wrapper to extract credentials
					// extract into variables: usernameVariable and passwordVariable
					//
					// withCredentials([<object syntax>])
					// {<block of code>}

					/* Example:
					withCredentials([
						usernamePassword(credentials: '<jenkins credentials>', usernameVariable: USER, passwordVariable: PWD)
					]) {
						// Can use extracted vars inside this block

						// example:
						// sh "<various shell commands> ${USER} ${PWD}}"

					} //withCredentials
					*/
				}
			}
		}

		stage('2 - Build') {

                        steps {
                        	script {
					echo '2: Build Image'
					//dockerImage = docker.build nginxImage
				}
                        }
                }

		stage('3 - Test') {

			// execute steps when:
			when {
                        	// must contain expression to say when:
                                expression {
                                        // expression
                                        // example:
                                        // params.executeTests == true
                                        //
                                        // can also omit the ==, it will assume true
                                        // params.executeTests

					params.executeTests // execute only if executeTests says true

                                }
                        } // when

                        steps {
                        	script {
					echo '3: Test'
					echo "Testing version: ${params.VERSION}"
				}
                        }
                }

		stage('4 - Push') {

                        steps {
                        	script {
					echo '4: placeholder'
				}
                        }
                }
	
	} // stages

	post {
	// Executes following steps after all stages are complete
	// Conditions:

		always {
		// always execute
			echo 'Post operations'
		}

		success {
		// in case of success
			echo 'Post operations after success'

		}

		failure {
		// in case of failure
			echo 'Post operations after failure'
		}
	}
}