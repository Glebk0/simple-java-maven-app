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
        secretEnvVar(key: 'DOCKER_PASSWORD', secretName: 'docker-regestry-credentials', secretKey: 'password'),
        envVar(key: 'DOCKER_REGESTRY_URL', value: 'docker.artem.services'),
        envVar(key: 'DOCKER_REPO', value: 'artem')
      ]
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
      git 'https://git.artem.services/artem/maven-project.git'
      container('maven') {
        stage('Build a Maven project') {
          sh 'mvn -B clean install'
        }
      }
    }
  }
}