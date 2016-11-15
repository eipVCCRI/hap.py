node {
	stage 'Checkout'

	checkout scm

    stage 'Build / Install'

    sh 'cd ${WORKSPACE} && /illumina/sync/software/groups/hap.py/latest/python-ve/bin/python-wrapper.sh install.py ${WORKSPACE}/install --setup illumina --python system --python-interpreter /illumina/sync/software/groups/hap.py/latest/python-ve/bin/python-wrapper.sh'

    stage 'Test'

    sh 'cd ${WORKSPACE}/install && PYTHON=/illumina/sync/software/groups/hap.py/latest/python-ve/bin/python-wrapper.sh ${WORKSPACE}/src/sh/run_tests.sh'
    
    stage 'Notify'
        emailext body: 'The build was run.', recipientProviders: [[$class: 'CulpritsRecipientProvider'], [$class: 'DevelopersRecipientProvider']], subject: 'Build notification'
}