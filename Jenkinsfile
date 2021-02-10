#!groovy
@Library("jenkinslib@master") _

// 实例化共享库
def build = new org.devops.build()
def tools = new org.devops.tools()

// 环境变量
String srcUrl = "${env.srcUrl}"
String branchName = "${env.branchName}"
String buildType = "${env.buildType}"
String buildShell = "${env.buildShell}"

// 流水线
pipeline {
    agent any

    stages {
        
        stage("CheckOut"){
            steps{
                script{
                    tools.PrintMes("获取代码","green")
                    checkout([$class: 'GitSCM', branches: [[name: '${branchName}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'gitlab', url: '${srcUrl}']]])
                }
            }
        }
        
        stage("Build"){
            steps{
                script{
                    tools.PrintMes("构建打包","green")
                    build.Build(buildType,buildShell)
                }
            }
        }
    }
}
