// Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'YOUR_REPOSITORY_URL' // Replace with your repository URL
            }
        }

        stage('Build Application') {
            steps {
                sh 'python app.py &' // Run the Flask app in the background
                sh 'sleep 5'        // Give the app some time to start
            }
        }

        stage('Performance Test') {
            steps {
                sh 'mkdir -p jmeter-results'
                sh 'java -jar /path/to/apache-jmeter-X.X.X/bin/ApacheJMeter.jar -n -t hello_world_test.jmx -l jmeter-results/report.jtl'
            }
        }

        stage('Publish Performance Report') {
            steps {
                performanceReport publishers: [jmeterPublisher(sourceFile: 'jmeter-results/report.jtl')]
            }
        }

        stage('Stop Application') {
            steps {
                sh 'pkill -f app.py' // Kill the Flask app process
            }
        }
    }
}