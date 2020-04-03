podTemplate(
  containers: [
    containerTemplate(
      name: 'maven',
      image: 'maven:latest',
      command: 'cat',
      ttyEnabled: true),
    containerTemplate(
      name: 'docker',
      image: 'docker:latest',
      command: 'cat',
      ttyEnabled: true,
      envVars: [
        secretEnvVar(key: 'DOCKER_LOGIN', secretName: 'docker-regestry-credentials', secretKey: 'username'),
        secretEnvVar(key: 'DOCKER_PASSWORD', secretName: 'docker-regestry-credentials', secretKey: 'password')
    )
  ],
  volumes: [
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