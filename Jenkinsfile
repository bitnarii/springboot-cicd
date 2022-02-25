pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build done1'
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        echo 'upload done2'
        sh 'aws s3 cp build/libs/application.war s3://springboot-cicd-bitnarii/application.war --region us-west-2' 
      }
    }
    // s3이름이랑 리전

    stage('deploy') {
      steps {
        echo 'deploy done3'
                         sh 'aws elasticbeanstalk create-application-version --region us-west-2 --application-name springboot-cicd-bitnarii --version-label ${BUILD_TAG} --source-bundle S3Bucket="springboot-cicd-bitnarii",S3Key="application.war"' 
                 sh 'aws elasticbeanstalk update-environment --region us-west-2 --environment-name Springbootcicdbitnarii-env --version-label ${BUILD_TAG}' 
      }
    }
    // 리전2, 어플리케이션이름 : 빈스톡 어플리케이션이름, 환경이름 : 빈스톡 환경이름
  }
}