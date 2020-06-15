pipeline {
   agent any
	stages {
		stage('Git Checkout'){
			steps {
				git 'https://github.com/madhumita-kundo/Database-service.git'
				}
		}
		stage('validate'){
			steps {
				echo "validate database changes"
				}
		}
    		stage('test'){
			steps {
				echo "connect to a test database and run test script"
				}
		}
		stage('package'){
			steps {
				echo "run the build script"
				}
		}
		stage('publish artifacts to udeploy'){
			  step([$class: 'UCDeployPublisher',
        siteName: '35.242.161.163',
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            componentName: 'database Service Component',
         delivery: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
                pushVersion: '$componentName_${BUILD_NUMBER}',
                baseDir: '\\workspace\\web\\targets',
                fileIncludePatterns: '*.sql',
                fileExcludePatterns: '',
                pushProperties: 'jenkins.server=Local\njenkins.reviewed=false',
                pushDescription: 'Pushed from Jenkins',
                pushIncremental: false
            ]
        ]
    ])
}
		stage('deploy to UcDeploy'){
			 steps([$class: 'UCDeployPublisher',
        			siteName: '35.242.161.163',
        			component: [
            			$class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            			componentName: 'Database Service Component'
       				 ],
       				 deploy: [
            			$class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',
           			 deployApp: 'Full Application',
           			 deployEnv: 'DEV',
            			deployProc: 'Deploy Application',
           			 deployVersions: '${component_name}_${BUILD_NUMBER}',
           			 deployOnlyChanged: false
        ]
    ])
}
	}
}
