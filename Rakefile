# encoding: utf-8

require "rubygems"
require "bundler/setup"
require "stringex"

domain          = "timboskitchen.com"

public_dir      = "public"  # compiled site directory
source_dir      = "source"  # source file directory
posts_dir       = "_posts"  # directory for blog files
server_port     = "4000"    # port for preview server eg. localhost:4000

desc "Begin a new post in #{source_dir}/#{posts_dir}"
task :new_post, :title do |t, args|
    mkdir_p "#{source_dir}/#{posts_dir}"
    args.with_defaults(:title => 'new-post')
    title = args.title
    filename = "#{source_dir}/#{posts_dir}/#{Time.now.strftime('%Y-%m-%d')}-#{title.to_url}.md"
    if File.exist?(filename)
        abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
    end
    puts "Creating new post: #{filename}"
    open(filename, 'w') do |post|
        post.puts "---"
        post.puts "layout: post"
        post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
        post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
        post.puts "categories: "
        post.puts "---"
    end
end

desc "Generate jekyll site"
task :generate do
    puts "## Generating Site with Jekyll"
    system "compass compile --css-dir #{source_dir}/assets/css"
    system "jekyll ./#{source_dir} ./#{public_dir}"
end

desc "Preview the site in a web browser"
task :preview do
    jekyll_pid = Process.spawn("jekyll ./#{source_dir} ./#{public_dir} --server #{server_port}")
    compass_pid = Process.spawn("compass watch --css-dir #{source_dir}/assets/css")

    puts "Starting to watch source with Jekyll (PID: #{jekyll_pid}) and Compass (PID: #{compass_pid})."
    puts "Visit your site in a browser at http://localhost:#{server_port}. Press Ctrl-C to stop…\n\n"

    trap("SIGINT") do
        print "\nKilling dem processes…\t\t"
        [jekyll_pid, compass_pid].each { |pid| Process.kill(9, pid) rescue Errno::ESRCH }
        puts "DONE!\n"
        exit 0
    end

    [jekyll_pid, compass_pid].each { |pid| Process.wait(pid) }
end
