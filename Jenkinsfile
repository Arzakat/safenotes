pipeline {
    agent any

    stages {
        //Etapa 1: Clonar repositorio
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Arzakat/safenotes.git'
            }
        }

        // Etapa 2: Instalar dependencias
        stage('Install Dependencies') {
            steps {
                bat 'npm install'  // en Windows es bat
            }
        }

        // Etapa 3: Análisis OWASP
        stage('Análisis de Dependencias') {
            steps {
                bat 'if not exist "dependency-check-report" mkdir dependency-check-report'
                tool 'mi-primer-dependency-check'
                dependencyCheck odcInstallation: 'mi-primer-dependency-check', additionalArguments: '--project "safenotes" --scan "target" --format "HTML" --format "XML" --out "dependency-check-report" --enableExperimental'
            }
        }

        // Etapa 4: Ejecutar tests
        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
    }
}