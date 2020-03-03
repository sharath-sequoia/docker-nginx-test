pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
/*
    parameters {
        string(name: 'tag', defaultValue: '1.0', description: 'Which tag/branch to build?')
        choice(name: 'environment', choices: ['dev', 'staging', 'uat', 'pre-production', 'production'], description: 'Deploy to which environment?')
    }

*/

    parameters {
            choice(name: "CHOICE", choices: createChoicesWithPreviousChoice(["foo", "bar", "baz"], "baz").join("\n"))
    }

    stages {
        stage('env set')
        {
          steps{
            script{
              env.BUILD_CAUSE = currentBuild.getBuildCauses()[0].shortDescription.contains("push by") ? 'push' : 'manual'
            }
          }
        }

        stage('Stage1')
        {
          when {
              expression { env.BUILD_CAUSE == 'manual' }
          }
          steps{
            script{
              def causes = currentBuild.getBuildCauses()
              echo causes.toString()
              //echo "Hello world!"
              def cause = currentBuild.getBuildCauses()[0].shortDescription.contains("push by") ? 'push' : 'manual'

              if( cause == 'push' )
              {
                echo "The build was caused by Git push"
              }
              else
              {
                echo "Build was NOT caused by Github push"
              }
            }
          }
        }
    }
}


def List createChoicesWithPreviousChoice(List defaultChoices, String previousChoice) {
    if (previousChoice == null) {
       return defaultChoices
    }
    choices = defaultChoices.minus(previousChoice)
    choices.add(0, previousChoice)
    return choices
}
