
gitHubUser = "epy1234"
gitHubUser = "${params.gitUserName}"

pipeline {
    agent any

    stages {
        stage('echo pm'){
            steps {
                script {
                    
                   properties([parameters([string(defaultValue: 'epy1234', description: 'git user name', name: 'gitUserName'), [$class: 'CascadeChoiceParameter', choiceType: 'PT_SINGLE_SELECT', description: 'Select the Repository from the Dropdown List', filterLength: 1, filterable: false, name: 'REPO', randomName: 'choice-parameter-18506770003900', referencedParameters: 'gitUserName', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return[\'Could not get The Repos\']'], script: [classpath: [], sandbox: false, script: '''import groovy.json.JsonSlurper
def get = new URL("https://api.github.com/users/${gitUserName}/repos").openConnection();
def getRC = get.getResponseCode();

if (getRC.equals(200)) {
    def json = get.inputStream.withCloseable { inStream ->
        new JsonSlurper().parse( inStream as InputStream )
    }

    def item = json;
    def names = [];

    item.each { repo ->
        names.push(repo.name);
    }   
    return names;
    
}''']]], [$class: 'CascadeChoiceParameter', choiceType: 'PT_SINGLE_SELECT', description: 'Select the Branch from the Dropdown List', filterLength: 1, filterable: false, name: 'BRANCH', randomName: 'choice-parameter-18506776678100', referencedParameters: 'REPO,gitUserName', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return[\'Could not get Branch from the Repo\']'], script: [classpath: [], sandbox: false, script: '''import groovy.json.JsonSlurper
def getBranches = new URL("https://api.github.com/repos/${gitUserName}/" + REPO + "/branches").openConnection();
def getRCBranches = getBranches.getResponseCode();

if (getRCBranches.equals(200)) {
   def jsonBr = getBranches.inputStream.withCloseable { inStream ->
           new JsonSlurper().parse( inStream as InputStream )
   }

    def itemBr = jsonBr;
    def namesBr = [];

    itemBr.each { branch ->
        namesBr.push(branch.name);
    } 
    return namesBr;
}''']]]])])
                }
            
                echo "${gitUserName}"
                //echo "https://api.github.com/users/${gitHubUser}/repos"
                echo "https://api.github.com/repos/${gitUserName}/" + REPO + "/branches"
            }
            
        }
    }
}
  
