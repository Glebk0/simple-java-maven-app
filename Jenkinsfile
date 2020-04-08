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
      mountPath: '/root/.m2nrepo', 
      claimName: 'maven-repo', 
      readOnly: false),
    secretVolume(
      secretName: 'mvn-settings',
      mountPath: '/root/.m2/')]
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