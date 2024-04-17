```shell
pipeline {
    agent any
    
    parameters {
        choice choices: ['all', 'psy', 'prepsy', 'szrhopesen'], description: '部署目标', name: 'TARGET'
        choice choices: ['stage', 'prod'], description: '环境', name: 'ENV'
        gitParameter branch: '', branchFilter: 'origin/(.*)', defaultValue: 'main', description: '分支名称', name: 'BRANCH_NAME', quickFilterEnabled: false, selectedValue: 'NONE', sortMode: 'NONE', tagFilter: '*', type: 'GitParameterDefinition'
        choice choices: ['151 Test Server', '47.106.32.164 Prod Server', '120.24.233.31 Production Server'], description: '部署目标服务器', name: 'DEPLOY_SERVER'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${params.BRANCH_NAME}", credentialsId: '78b1c420-a9c3-4c92-a5c8-eccb9441371c', url: 'http://39.108.113.20:51110/lab/ruoyi-monorepo.git'
            }
        }
        stage('BuildAll') {
            when {
                expression { params.TARGET ==~ /(all)/ }
            }
            steps {
                nodejs('v16.14.0') {
                    // some block
                    sh 'pnpm install  --no-frozen-lockfile'
                    sh "pnpm run build:${params.ENV}"
                    sh 'tar -zcvf szr-dist.tar.gz website/szr-vue/dist/'
                    sh 'tar -zcvf ai.psychological.vue.tar.gz website/ai.psychological.vue/dist/'
                    sh 'mkdir -p historyfile'
                    sh 'cp szr-dist.tar.gz historyfile/szr-dist-$(date +%Y%m%d%H%M%S).tar.gz'
                    sh 'cp psychological-dist.tar.gz historyfile/psychological-dist-$(date +%Y%m%d%H%M%S).tar.gz'
                }
            }
        }
        stage('BuildSzr') {
            when {
                expression { params.TARGET ==~ /(szr|szrhopesen)/ }
            }
            steps {
                nodejs('v16.14.0') {
                    // some block
                    sh 'pnpm install  --no-frozen-lockfile'
                    sh "pnpm run build:${params.ENV}:szr"
                    sh 'tar -zcvf szr-dist.tar.gz website/szr-vue/dist/'
                    sh 'mkdir -p historyfile'
                    sh 'cp szr-dist.tar.gz historyfile/szr-dist-$(date +%Y%m%d%H%M%S).tar.gz'
                }
            }
        }
        stage('BuildPsy') {
            when {
                expression { params.TARGET ==~ /(psy)/ }
            }
            steps {
                nodejs('v16.14.0') {
                    // some block
                    sh 'pnpm install  --no-frozen-lockfile'
                    sh "pnpm run build:${params.ENV}:ai"
                    sh 'tar -zcvf psychological-dist.tar.gz website/ai.psychological.vue/dist/'
                    sh 'mkdir -p historyfile'
                    sh 'cp psychological-dist.tar.gz historyfile/psychological-dist-$(date +%Y%m%d%H%M%S).tar.gz'
                }
            }
        }
        stage('DeployAllOrSzr') {
            when {
                expression { params.TARGET ==~ /(all|szr)/ }
            }
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: "${params.DEPLOY_SERVER}", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/nginx/projects/szr/szr-admin
                tar -zxvf szr-dist.tar.gz --strip-components 3
                rm -rf szr-dist.tar.gz szr-dist.tar.gz''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/nginx/projects/szr/szr-admin', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'szr-dist.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('DeployAllOrSzrHopesen') {
            when {
                expression { params.TARGET ==~ /(all|szrhopesen)/ }
            }
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: "${params.DEPLOY_SERVER}", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/nginx/projects/szr/szr-hopesen
                tar -zxvf szr-dist.tar.gz --strip-components 3
                rm -rf szr-dist.tar.gz szr-dist.tar.gz''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/nginx/projects/szr/szr-hopesen', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'szr-dist.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('DeployAllOrPsy') {
            when {
                expression { params.TARGET ==~ /(all|psy)/ }
            }
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: "${params.DEPLOY_SERVER}", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd  /usr/share/nginx/html/psychological/admin
                tar -zxvf psychological-dist.tar.gz --strip-components 3
                rm -rf psychological-dist.tar.gz''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/usr/share/nginx/html/psychological/admin', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'psychological-dist.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('DeployPrepsy') {
            when {
                expression { params.TARGET ==~ /(prepsy)/ }
            }
            steps {
                nodejs('v16.14.0') {
                    // some block
                    sh 'pnpm install  --no-frozen-lockfile'
                    sh "pnpm run build:${params.ENV}:ai"
                    sh 'tar -zcvf prepsy-dist.tar.gz website/ai.psychological.vue/dist/'
                    sh 'mkdir -p historyfile'
                    sh 'cp prepsy-dist.tar.gz /usr/share/nginx/html/psychological/admin'
                    sh 'cp prepsy-dist.tar.gz historyfile/prepsy-dist-$(date +%Y%m%d%H%M%S).tar.gz'
                    sh 'cd /usr/share/nginx/html/psychological/admin && tar -zxvf prepsy-dist.tar.gz --strip-components 3'
                }
            }
        }
    }
}

```

