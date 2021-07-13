# Warn when there is a big PR
fail("Big PR. Please split this pull request.") if git.lines_of_code > 500

# Tests
Dir["**/test-results/**/*.xml"].each do |file_name|
  junit.parse file_name
  junit.report
end

# AndroidLint
Dir["**/reports/lint-results*.xml"].each do |file_name|
  android_lint.skip_gradle_task = true
  android_lint.filtering = true
  android_lint.report_file = file_name
  android_lint.lint(inline_mode: true)
end

# Ktlint
checkstyle_format.base_path = Dir.pwd
Dir["**/reports/ktlint/ktlintMainSourceSetCheck/**.xml"].each do |file_name|
  checkstyle_format.report file_name
end

# Detekt
Dir["**/reports/detekt/detekt.xml"].each do |file_name|
  kotlin_detekt.severity = "warning"
  kotlin_detekt.gradle_task = "detekt"
  kotlin_detekt.report_file = file_name
  kotlin_detekt.detekt(inline_mode: true)
end