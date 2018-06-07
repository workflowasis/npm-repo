pipeline {
  agent any
  stages {
    stage('Build Demo App') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''npm install
npm run build
ls'''
      }
    }
    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }
    stage('Upload to Artifactory') {
      steps {
        sh 'curl -uadmin:APBcyn5vVoefw71T -T /tmp/jenkins/workspace/Shayki_master-KKIFYO5SNM5S43SC4PZRON5JVDZNLUGBTT6QRAJUESJJW2LMXOLA/nodejs-demoapp.zip "http://35.205.54.43:8081/artifactory/generic-local/shayki"'
      }
    }
    stage('Deploy Dev') {
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
ansible-playbook playbooks/deploy_dev.yml'''
      }
    }
  }
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
    Stage
''', description: 'Type of action to perform')
  }
}