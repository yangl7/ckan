pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'python:2-alpine' 
                    image 'postgres:10'
                }
            }
            environment {
                CKAN_DATASTORE_POSTGRES_DB = 'datastore_test'
                CKAN_DATASTORE_POSTGRES_READ_USER = 'datastore_read'
                CKAN_DATASTORE_POSTGRES_READ_PWD = 'pass'
                CKAN_DATASTORE_POSTGRES_WRITE_USER = 'datastore_write'
                CKAN_DATASTORE_POSTGRES_WRITE_PWD = 'pass'
                CKAN_POSTGRES_DB = 'ckan_test'
                CKAN_POSTGRES_USER = 'ckan_default'
                CKAN_POSTGRES_PWD = 'pass'
                PGPASSWORD = 'ckan'
                NODE_TESTS_CONTAINER = '2'
                NOSETEST_COMMON_OPTIONS = '-v --ckan --reset-db --with-pylons=test-core-circle-ci.ini --nologcapture --with-coverage --cover-package=ckan --cover-package=ckanext --with-xunit --xunit-file=/root/junit/junit.xml ckan ckanext'
            }
            steps {
                sh 'python -m py_compile bin/running_stats.py' 
            }
        }
    }
}

