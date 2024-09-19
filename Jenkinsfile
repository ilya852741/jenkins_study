pipeline {
    agent any
    triggers {
        parameterizedCron('''*/5 * * * * ''')
    }
    parameters {
        choice(
                name: 'scenario',
                choices: [
                        '',
                        'clean_build_without_cache',
                        'clean_build_with_remote_cache',
                        'rebuild_without_changes',
                        'rebuild_changed_celebrity_module',
                        'rebuild_changed_feature_module'
                ],
                description: 'Сценарий (для прогона всех сценариев выберите пустой вариант)'
        )
    }
    stages {
        stage("prepare") {
            steps {
                echo "prepare stage"
            }
        }
        stage("profile") {
            steps {
                echo "profile stage"
            }
        }
    }
    post {
        always {
            script {
                // if (currentBuild.getCause(hudson.model.Cause$UserCause)) {
                    // echo "Build was triggered by user, scenario = $params.scenario"
                echo "Build was triggered by ${currentBuild.getCause(hudson.model.Cause$UserCause)}"
                // } else {
                  // echo "Build was triggered NOT by user, scenario = $params.scenario"
                // }
            }
        }
        cleanup {
            deleteDir()
        }
    }
}
