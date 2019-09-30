pipeline {
    // agent 指示 Jenkins 为 Pipeline 分配执行程序和工作空间
    agent { docker 'python:3.5.1' }

    // 设置环境变量
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'mysql'
    }

    stages {
        stage('build') {
            steps {
                sh 'python --version'
                echo "hello world!"
		// 打印全部的环境变量
		// sh 'printenv'
            }
        }
        stage('Test') {
            steps {
		// 打印指定的环境变量
		print(env.DB_ENGINE)
            }
        }
    }
    // 当 Pipeline 运行完成时，你可能需要做一些清理工作或者基于 Pipeline 的运行结果执行不同的操作， 这些操作可以放在 post 部分。
    post {
	// 总是执行
        always {
            echo 'This will always run'
	    // 通过 archiveArtifacts 步骤和文件匹配表达式可以很容易的完成构建结果记录和存储
	    // archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
	    // 收集我们的测试结果
	    junit 'reports/*.xml'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
