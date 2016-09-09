node {
  git url: 'https://github.com/nekromant/stlink.git'
  // FixMe: Hack
  sh 'git tag 999.9.9'
  sh 'rm -Rfv build;'
  sh "mkdir build; cd build; cmake ..; make"
  sh "cd build && ctest --no-compress-output -T Test || true"
  sh './scripts/run_clang_analyze.sh'

  step([$class: 'XUnitBuilder', testTimeMargin: '3000', thresholdMode: 1, thresholds: [[$class: 'FailedThreshold', failureNewThreshold: '2', failureThreshold: '2', unstableNewThreshold: '1', unstableThreshold: '1'], [$class: 'SkippedThreshold', failureNewThreshold: '2', failureThreshold: '2', unstableNewThreshold: '1', unstableThreshold: '1']], tools: [[$class: 'CTestType', deleteOutputFiles: true, failIfNotNew: true, pattern: 'build*/Testing/*/*.xml', skipNoTestFiles: false, stopProcessingIfError: true]]])
  step([$class: 'WarningsPublisher', canComputeNew: false, canResolveRelativePaths: false, consoleParsers: [[parserName: 'GNU C Compiler 4 (gcc)']], defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', messagesPattern: '', unHealthy: ''])

}
