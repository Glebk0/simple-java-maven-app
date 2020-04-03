podTemplate(
  containers: [
    containerTemplate(
      name: 'maven',
      image: 'maven:latest',
      command: 'cat',
      ttyEnabled: true)
  ],
  volumes: [
    persistentVolumeClaim(
      mountPath: '/root/.m2/repository', 
      claimName: 'maven-repo', 
      readOnly: false),
    hostPathVolume(
      hostPath: '/var/run/docker.sock',
      mountPath: '/var/run/docker.sock')]
)
{
  node(POD_LABEL) {
    stage('Get a Maven project') {
      git 'https://github.com/Glebk0/simple-java-maven-app.git'
      container('maven') {
        stage('Build a Maven project') {
          sh 'mvn -B clean install'
        }
      }
    }
  }
}