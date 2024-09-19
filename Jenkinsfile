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

                echo "BUILD CAUSES START"
                echo "${currentBuild.getBuildCauses()}" //Always returns full Cause
                echo "${currentBuild.getBuildCauses('jenkins.branch.BranchEventCause')}" // Only returns for branch events
                echo "${currentBuild.getBuildCauses('hudson.triggers.SCMTrigger$SCMTriggerCause')}" // Only returns SCM Trigger
                echo "${currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')}"  // Only returns if user initiates via Jenkins GUI
                echo "${currentBuild.getBuildCauses('hudson.model.Cause$UserCause')}"  // Only returns if user initiates via Jenkins GUI
          
                def GitPushCause = currentBuild.getBuildCauses('jenkins.branch.BranchEventCause')
                def UserCause = currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')

                echo "BUILD CAUSES UserCause = $UserCause"
                echo "BUILD CAUSES END"
                
                // if (currentBuild.getCause(hudson.model.Cause$UserCause)) {
                    // echo "Build was triggered by user, scenario = $params.scenario"
                echo "Build was triggered by ${currentBuild.getBuildCauses(hudson.model.Cause$UserIdCause)}"
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
