pipeline {
    agent{
        node{
            label 'built-in'
            customWorkspace '/mnt/build/my-app/Q2-2026'
            
        }
    }
    stages {
                stage ('SCM') {
                    steps{
                     sh '''
                        rm -rf ./*
                        rm -rf .git
                        git clone https://github.com/shrutikadevops/my-app.git -b Q2-2026 .
                        '''
                }
                }
                
                stage ('build') {
                    steps{
                    sh '''
                    aws s3 cp index.html s3://shrutika-2001/Q2-2026/index.html
                    '''
                }
                }
                
                stage ('deploy') {
                    agent{
                    node{
                        label 'slave-1'
                        customWorkspace '/mnt/slave-1/Q2-2026'
                    }
                }
                steps{
                    sh '''
                    aws s3 cp s3://shrutika-2001/Q2-2026/index.html .
                    docker cp index.html server-1:/usr/local/apache2/htdocs
                    '''
                }
                }
                
            }
}
