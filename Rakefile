require 'bundler/setup'


$web_root = File.expand_path(".", Dir.pwd).gsub('/','\\')

desc "Build .Net appplication and Package using MSBuild"
task :build  do
	msbuild = "C:/Windows/Microsoft.NET/Framework/v4.0.30319/MSBuild.exe"
	sh "#{msbuild} FirstAspDotNetSolution.sln /t:Build /p:VisualStudioVersion=12.0 /p:DeployOnBuild=true"
end

# desc "Clean and Build from Albacore Task"
# msbuild :albaBuild do |cmd|
#   cmd.solution = "FirstAspDotNetSolution.sln"
#   cmd.targets = [:Clean, :Build]
#   cmd.properties = {:Configuration => "Debug"}
# end

desc "Deploy on IIS using MSDeploy"
task :deploy  do
	msdeploy =  "C:/Program Files/IIS/Microsoft Web Deploy V3/msdeploy.exe"
	sh "FirstAspDotNetApp/obj/Debug/Package/FirstAspDotNetApp.deploy.cmd /Y"
end

desc "Remove all build Files"
task :clean  do
	msbuild = "C:/Windows/Microsoft.NET/Framework/v4.0.30319/MSBuild.exe"
	sh "#{msbuild} FirstAspDotNetSolution.sln /t:Clean /p:VisualStudioVersion=12.0 " 
end


desc "Download nuget.exe"
task :setup do
	nuget = "https://www.nuget.org/nuget.exe"
	sh "curl -O #{nuget}"
end	


desc "Build and Deploy"
task :default => [:clean, :build, :deploy]

desc "Nuget Install"
task :nuget_install  do
	nuget_exe = "#{$web_root}/tools/nuget.exe"
	destination_directory = "#{$web_root}/FirstAspDotNetApp/packages.config"
	output_directory = "#{$web_root}\\packages"
	sh "#{nuget_exe} install #{destination_directory} -o #{output_directory}"
end