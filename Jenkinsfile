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
                    dir ('meta-raspberrypi') {
                        git branch: 'sumo', url: 'git://git.yoctoproject.org/meta-raspberrypi'
                    }
                }
            }
        }
        stage('Build') {
            steps {
               dir ('poky') {
                sh '''bash -c "source oe-init-build-env && bitbake-layers add-layer ../meta-example && bitbake-layers add-layer ../meta-raspberrypi && export MACHINE=\"raspberrypi3\" && bitbake minimal-example" '''
                }
            }
        }            
    }
}
