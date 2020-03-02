pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

    stages {

        stage('Stage1')
        {
            def causes = currentBuild.getBuildCauses()
            echo causes.toString()
            echo "Hello world!"
        }
    }
}
