#!groovy
@Library('roboshop-shared-library') _

// responsibility to pass what type of application and component is  this to pipeline decission

def configMap = [
    application: "nodejsVM",
    component: "catalogue"
]

if( ! env.BRANCH_NAME.equalsIgnoreCase('main')){
    pipelineDecission.decidePipeline(configMap)
}
else{
    echo "this is production , deal with CR process"
}