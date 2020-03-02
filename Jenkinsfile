pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('Stage1')
        {
          steps{
            script{
              def causes = currentBuild.getBuildCauses()
              echo causes.toString()
              echo "Hello world!"

              if( causes.toString().contains("push by") )
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
