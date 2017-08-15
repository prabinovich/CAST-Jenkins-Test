slackSend channel: "#smallfibonacci", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"

stage('Deploy approval'){
    input "Deploy to prod?"
}

node ('Docker-Build-Box') {
   stage ('Get Code') {
        git credentialsId: '1b132c46-025f-4c76-986d-91b3237c7c1f', url: 'https://gitlab.com/johnny2136/SmallFibonacci.git'
   }

   parallel (
     "stream 1" : {    
         stage ('Build App') {
                sh 'javac -d bin -cp "src/lib/*" src/fibo/Fibonacci.java src/fibo/FibonacciTest.java'
         }
     },
     "stream 2" : { 
          stage ('Unit Tests') {
                dir ("bin") {
                    sh 'java -cp .:../src/lib/* org.junit.runner.JUnitCore fibo.FibonacciTest'
                }
          }
     }
   )
}

slackSend channel: "#smallfibonacci", message: "Build Completed: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
