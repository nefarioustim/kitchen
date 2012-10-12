require "rubygems"
require "bundler/setup"
require "stringex"

domain          = "timboskitchen.com"

public_dir      = "public"  # compiled site directory
source_dir      = "source"  # source file directory
posts_dir       = "_posts"  # directory for blog files
new_post_ext    = "md"      # default new post file extension when using the new_post task
new_page_ext    = "md"      # default new page file extension when using the new_page task
server_port     = "4000"    # port for preview server eg. localhost:4000

desc "Begin a new post in #{source_dir}/#{posts_dir}"
task :new_post, :title do |t, args|
    mkdir_p "#{source_dir}/#{posts_dir}"
    args.with_defaults(:title => 'new-post')
    title = args.title
    filename = "#{source_dir}/#{posts_dir}/#{Time.now.strftime('%Y%m%d')}-#{title.to_url}.#{new_post_ext}"
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
    system "jekyll #{source_dir} #{public_dir}"
end
