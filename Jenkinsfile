@Library('jenkins-test-lib') _

def configMap = [
    project: "roboshop"
    component: "catalogue"
]

echo "Starting pipeline for ${configMap.project}/${configMap.component}"

if (env.BRANCH_NAME.equalsIgnoreCase('main')) {
    echo "test later"

} else {
    testpipeline(configMap) 
}

