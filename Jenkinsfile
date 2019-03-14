pipeline {
    agent any
    stages {
        stage('Fetch'){
            steps{
                sh 'echo "Yocto Fetch"'
                dir ('poky') {
                    git branch: 'sumo', url: 'http://git.yoctoproject.org/git/poky.git'
                    dir ('meta-example') {
                        git branch: 'master', url: 'https://github.com/abhinema/meta-example.git'
                    }
                }
            }
        }
        stage('Build') {
            steps {
               dir ('poky') {
                sh '''bash -c "export MACHINE=raspberrypi3 && source oe-init-build-env && bitbake-layers add-layer ../meta-example && bitbake-layers add-layer ../meta-raspberrypi && bitbake minimal-example" '''
                }
            }
        }            
    }
}
