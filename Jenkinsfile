stage('Deploy approval'){
    input "Deploy to prod?"
}

node ('Docker-Build-Box') {
   stage ('Get Code') {
        git credentialsId: '1b132c46-025f-4c76-986d-91b3237c7c1f', url: 'https://gitlab.com/johnny2136/SmallFibonacci.git'
   }

   stage ('Build App') {
        sh 'javac -d bin -cp "src/lib/*" src/fibo/Fibonacci.java src/fibo/FibonacciTest.java'
   }
}
