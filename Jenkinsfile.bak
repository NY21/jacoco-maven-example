pipeline {
	agent any

	stages {

		stage('Clear Workspace') {
			steps {
				echo 'Clearing Workspace'
				deleteDir()
			}
		}

		stage('Checkout') {
			steps {
				echo 'Checkout from scm'
				checkout scm
			}
		}

		/*stage('Build/Test/SonarScan') {
			steps {
				def sonar_proj_name=4182_GDP_Finance
				echo 'Build/Test/SonarScan'
				bat 'mvn --settings C:\\.m2\\FCA\settings.xml clean verify sonar:sonar -p1 !GDPFinanceear'
			}
		}*/

		stage('Publish TestResults') {
			steps {
				echo 'Publish Test Results'
				step([$class: 'JUnitResultArchiver', testResults: '**/target/reports/TEST-*.xml'])
				//step([$class: 'JUnitResultArchiver', testResults: 'reports/junit/appJunitTest.xml'])
				publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'reports/jacoco', reportFiles: 'index.html', reportName: 'Jacoco Report', reportTitles: 'Jacoco Report'])
			}
		}

		/*stage('Push to Artifactory') {
			steps {
				def app-groupname='GDPFinance-group'
				echo 'Push to Artifactory'
				bat "mvn --settings C:\\.m2\\FCA\\settings.xml -DdevelopmentVersion=1.0.${BUILD_NUMBER}-SNAPSHOT -DreleaseVersion=1.0.${BUILD_NUMBER} -Dscm_username=t3669tb --batch-mode -Darguments=-Dmaven.test.skip=true release:prepare release:perform -Darguments='-Dmaven.javadoc.skip=true' -Dtag=MSR-${BUILD_NUMBER} -Dgoals=deploy -DreleaseVersion=1.0.${BUILD_NUMBER} -DdevelopmentVersion=1.0.${BUILD_NUMBER}-SNAPSHOT -Dusername=t3669tb -Dpassword=67459f37b7b5cc827e78394442c412c651299fa9"
			}
		}*/
			
	}
}
