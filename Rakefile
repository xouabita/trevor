require 'haml'
require 'fileutils'

def haml file
	dir_name  = File.dirname(file)
	out_name  = File.basename(file,'.haml') + ".html"
	html      = File.open(file, 'r') { |f| Haml::Engine.new(f.read).render }
	File.open(File.join(dir_name, out_name), 'w') { |f| f.write html }
end 

desc 'Build haml files'
task :build_haml do
	Dir.glob("./**/*.haml") do |file|
		haml(file)
	end
end

desc 'Build sass files'
task :build_sass do
	sh "sass --update sass:css"
end

desc 'Build all haml and sass files then build jekyll site'
task :build => [:build_sass, :build_haml] do
	sh "jekyll build"
end

desc 'Clean all the files'
task :clean do
	if File.exist?('./_site') then FileUtils.rm_rf './_site' end
	if File.exist?('./css')   then FileUtils.rm_rf './css' end
	FileUtils.rm Dir.glob('./**/*.html')
end