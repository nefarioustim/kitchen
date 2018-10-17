# encoding: utf-8

require "rubygems"
require "bundler/setup"
require "stringex"
require "highline/import"

domain          = "nefariousdesigns.co.uk"

public_dir      = "public"  # compiled site directory
source_dir      = "source"  # source file directory
posts_dir       = "_posts"  # directory for blog files
server_port     = "4000"    # port for preview server eg. localhost:4000
remote_server   = "pegasus" # remote server for deployment
remote_path     = "sites/zeta/public"    # remote path for deployment

def yesno(prompt = 'Continue?', default = true)
    a = ''
    s = default ? '[Y/n]' : '[y/N]'
    d = default ? 'y' : 'n'
    until %w[y n].include? a
        a = ask("#{prompt} #{s} ") { |q| q.limit = 1; q.case = :downcase }
        a = d if a.length == 0
    end
    a == 'y'
end

desc "Begin a new post in #{source_dir}/#{posts_dir}"
task :new_post, :title do |t, args|
    mkdir_p "#{source_dir}/#{posts_dir}"
    args.with_defaults(:title => 'new-post')
    title = args.title
    filename = "#{source_dir}/#{posts_dir}/#{Time.now.strftime('%Y-%m-%d')}-#{title.to_url}.md"
    if File.exist?(filename)
        abort("rake aborted!") if !yesno("#{filename} already exists. Do you want to overwrite?", false)
    end
    print "Creating new post: #{filename}…\t"
    open(filename, 'w') do |post|
        post.puts "---"
        post.puts "layout: post"
        post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
        post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
        post.puts "categories: "
        post.puts "---"
    end
    puts "[DONE!]\n"
end

desc "Generate jekyll site"
task :generate do
    print "Generating Site with Jekyll…\t"
    system "compass compile --css-dir #{source_dir}/assets/css"
    system "jekyll build --source ./#{source_dir} --destination ./#{public_dir}"
    puts "[DONE!]\n"
end

desc "Preview the site in a web browser"
task :preview do
    jekyll_pid = Process.spawn("jekyll serve --source ./#{source_dir} --destination ./#{public_dir}")
    compass_pid = Process.spawn("compass watch --css-dir #{source_dir}/assets/css")

    puts "Starting to watch source with Jekyll (PID: #{jekyll_pid}) and Compass (PID: #{compass_pid})."
    puts "Visit your site in a browser at http://localhost:#{server_port}. Press Ctrl-C to stop…\n\n"

    trap("SIGINT") do
        print "\nKilling dem processes…\t"
        [jekyll_pid, compass_pid].each { |pid| Process.kill(9, pid) rescue Errno::ESRCH }
        puts "[DONE!]\n"
        exit 0
    end

    [jekyll_pid, compass_pid].each { |pid| Process.wait(pid) }
end

desc "Deploy the site to the configured remote destination"
task :deploy do
    if ENV['remote']
        remote_server = ENV['remote']
    end
    puts "Deploying site to #{remote_server}:#{remote_path}…\n"
    system "rsync -av ./#{public_dir}/ #{remote_server}:#{remote_path}"
    puts "[DONE!]\n"
end
