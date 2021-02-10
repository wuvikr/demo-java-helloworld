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
    
    options {
        timestamps()  //日志会有时间
        skipDefaultCheckout()  //删除隐式checkout scm语句
        disableConcurrentBuilds() //禁止并行
        timeout(time: 1, unit: 'HOURS')  //流水线超时设置1h
    }

    stages {
        
        stage("CheckOut"){
            steps{
                script{
                    tools.PrintMes("获取代码","green")
                    
                    if ("${runOpts}" == "GitlabPush"){
                        branchName = branch - "refs/heads/"
                    }

                    tools.PrintMes("${branchName}","red")
                    
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
