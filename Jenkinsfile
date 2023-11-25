pipeline {
    agent none
    stages {
        stage('Build') {
            agent { label 'aws-agent1' }
            steps {
                //sh 'python3.8 -m py_compile sources/prog.py sources/calc.py'
                sh 'sudo apt install docker.io -y'
                sh 'python3 --version'
                sh 'sudo apt install python3-pip -y'
                sh 'pip3 --version'
                sh 'ls -la'
                sh 'pip3 install -r theProject/requirements.txt'

                sh 'python3 -m py_compile theProject/run.py'
                stash(name: 'compiled-results', includes: 'theProject/run.py*')
            }
        }
        stage('Test') {
            agent { label 'aws-agent1' }
            steps {
                sh 'python3 -m pytest -v --junit-xml test-reports/results.xml ./theProject'
            }
            post {
                always {
                    junit "test-reports/results.xml"
                }
            }
        }
        stage('Deliver') {
            agent { label 'aws-agent1' }
            environment {
                //VOLUME = '$(pwd)/CI_CD_githubActions:/src'
                VOLUME = '$(pwd):/src'
                IMAGE = 'cdrx/pyinstaller-linux'
            }
            steps {
                //dir(path: "run/" + env.BUILD_ID) {
                //dir(path: "CI_CD_githubActions/" ) {
                    // unstash(name: 'compiled-results')
                    // sh "sudo docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F ../project2/CI_CD_githubActions/prog.py'"
                    //sh 'print('Volume: ', VOLUME)'
                    //sh "sudo docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F ../../CI_CD_githubActions/prog.py'"
                    sh 'sudo docker image build . -t py2bin:latest'
                    sh "sudo docker run --rm -v ${VOLUME} py2bin 'pyinstaller -F --hidden-import numpy --hidden-import tqdm theProject/run.py'"
                    sh 'pwd'
                    //sh 'pwd'
                    //sh 'ls -la'
                //}
                sh 'pwd'
                sh 'echo "hello deliver"'
            }
            post {
                success {
            //        archiveArtifacts "${env.BUILD_ID}/sources/dist/prog"
                     archiveArtifacts "dist/run"
           //         archiveArtifacts "CI_CD_githubActions/__pycache__/**"
           //         sh 'echo "hello deliver2"'
                }
            }
        }
        
    }
}
