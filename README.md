# xcode-issue

# Xcode16 이슈 조치

1. 파이어베이스 BoringSSL-GRPC / cocoapods setting
post_install do |installer|
  // Xcode 16 임시추가 부분
  installer.pods_project.targets.each do |target|
    if target.name == 'BoringSSL-GRPC'
      target.source_build_phase.files.each do |file|
        if file.settings && file.settings['COMPILER_FLAGS']
          flags = file.settings['COMPILER_FLAGS'].split
          flags.reject! { |flag| flag == '-GCC_WARN_INHIBIT_ALL_WARNINGS' }
          file.settings['COMPILER_FLAGS'] = flags.join(' ')
        end
      end
    end
  end
  // Xcode 16 임시추가 부분
end

2. 시뮬레이터로 빌드시 arm64로 인한 building failed 이슈 조치 방법
   model name (Rosetta) 지정 후 시뮬레이터 빌드 실행
