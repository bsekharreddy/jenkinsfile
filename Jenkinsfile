pipeline {
    agent any
    
    stages {
        stage("git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/bsekharreddy/simplecalc.git'
            }
        }
        stage('Cmake Build') {
        steps {
            sh 'cd /var/lib/jenkins/workspace/simplecalc'
            sh 'pwd'
            sh 'sudo -s cmake .'
            sh 'sudo -s make'
            sh 'sudo ./simplecalc'
            echo "CMake Build Success"
        }
    }
        
    }
    post {
    failure {
    script {
        print("post jenkins stage")
        def mail_recipient_int= "sekhar.b@ltts.com"

        env.mail_recipient=mail_recipient_int + env.GIT_COMMITTER_EMAIL

        print "Commiter Mail_ID"

        print ("${env.GIT_COMMITTER_EMAIL}")

        print ("${env.mail_recipient}")

            if (env.BRANCH_NAME != 'master') {

                emailext (

                        from: 'sekharlathas997@gmail.com',

                        mimeType: 'text/html',

                        subject: '$PROJECT_NAME - Build # $BUILD_NUMBER',

                        body: """Hi Committer and integration team,
                                    Please check the failed build at:
                                    ${env.BUILD_URL}
                                    """,

                        to: "${env.mail_recipient}"

                        )

                    }
        
    }
    }
}
}
