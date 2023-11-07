# source 'https://github.com/CocoaPods/Specs.git'
source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'

$project_name = 'Argus'

platform :ios, '12.0'

inhibit_all_warnings!

target $project_name do
	pod 'JLRoutes'
	pod 'Masonry'
	pod 'Protobuf'
	pod 'XLForm'

	post_install do |installer|
		$version = installer.podfile.root_target_definitions[0].platform.deployment_target.to_s.to_f
		installer.pods_project.targets.each do |target|
			target.build_configurations.each do |config|
				config.build_settings['CLANG_ANALYZER_LOCALIZABILITY_NONLOCALIZED'] = 'YES'
				if config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'].to_f < $version
					config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = $version.to_s
				end
			end
		end
		# Install acknowledgements
		$src = 'Pods/Target Support Files/Pods-%s/Pods-%s-acknowledgements.plist' % [$project_name, $project_name]
		$dst = '%s/Resources/Settings.bundle/Acknowledgements.plist' % $project_name
		FileUtils.cp_r($src, $dst, :remove_destination => true)
	end
end
